---
title: "JavaScript Promise 101 - Reasoning"
date: "2024-06-09"
categories: ["JavaScript"]
---



## Why Promise ?

To begin with, let's understand what is ? 

>   A Promise is **an object representing the eventual completion or failure of an asynchronous operation**. Since most people are consumers of already-created promises, this guide will explain consumption of returned promises before explaining how to create them.
>
>   [-- MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

and why we will need the concept of `Promise` ? 

>   1.   Promise provide you a way to **reducing call-back hell** 
>   2.   Promises give us the ability to **write cleaner code**
>   3.   Promise allow you to **handle error together** (or optionally by each promise)
>
>   [-- ColorCode - JavaScript Promises](https://www.youtube.com/watch?v=TnhCX0KkPqs) 







## **World without Promise ?**

#### Broken Async 

First, we begin with a simple asynchronous function `getWeather_1` using `setTimeout` that is **broken** (and we will be using this method to simulate the asynchrnouse function a lot in the upcoming examples). 

```javascript
// [ASYNC code (primitive with bug)]

function getWeather_1() {
	setTimeout(() => {
		return "Sunny";
	}, 1000);
}
let weather_1 = getWeather_1();
document.body.innerText(weather_1);

// What is wrong ?
// - this function will always set weather to "undefined"
// - this ie because function "getWeather"
//   will only return after the interval (delay=100) is met
```

#### Primitive Async

Second, let's try **fixing bug** in the previous asynchronouse code example: 

```javascript
// [ASYNC code (primitive)]

function getWeather_2() {
    setTimeout(() => {
        weather_2 = "Sunny";
        document.body.innerText(weather_2);
	}, 1000);
}
let weather_2;
getWeather_2();

// How this is fixed ?
// - now the set text "innerText" command will only execute
//   after the weather_2 varaible has been assigned with "Sunny"

// What is the wrong ?
// - now the function is a bit cluttered in a way it is both:
//   1. non-modular (both setText and getData are in the same place)
//   2. have side-effect (it will change the global variable weather_2)
```

#### Async Enhanced

Now we start to resolve the persisting issue with the code, first let's try tackle the problem of **side-effect** with **another function**:

```javascript
// [ASYNC code (with callback)]

function weatherReceived_nowChangeText(data){
    let weather = data;
    document.body.innerText(weather);
}
function getWeather_3(){
    setTimeout(()=>{
        let weather_3 = "Sunny";
        weatherReceived_nowChangeText(weather_3)
    }, 1000)
}
getWeather_3();

// What is solved ?
// - now the function has no side-effect,
// - and "seems" a bit modular now

// What's still wrong ?
// - the function only "seems" modular, but they are not !!!
//   because executing function "getWeather_3" will necessary update text via "weatherReceived_nowChangeText"
//   (i.e. you cannot use getWeather_3 to do anything else, say for intance to "console.log" or "alert")
// - the two function looks modular, but are in nature still tightly coupled
```

#### Async with callback 

Despite the side-effect, we can also **resolve the modularity (strong couple/dependency)** via **callback function**

```javascript
// [Async with callback]

function weatherReceived(data) {
    let weather = data;
    document.body.innerText(weather);
}

function getWeather(callback) {
    setTimeout(() => {
        callback('Sunny');
    }, 1000);
}
getWeather (weatherReceived)
getWeather ((data)=>{console.log(data)}) // [Example Alternative Callback - 1]
getWeather ((data)=>{alert(data)})       // [Example Alternative Callback - 2]

// What is solved ?
// - now the function is side-effect free
// - and in the meanwhile modular !
//   (you can pass in something differet like the two alternative example shown)

// What is still wrong ?
// - despite it have solved the previous issue about "side-effect" and "modularity/dependency"
//   you could likely face the "callback hell" showcased next ....
```

#### Async with callback hell

using callback is benificial, but can result in **callback hell **(or **Pyramid of doom**, **Heavy nesting**, **Deeply nested callbacks**): 

```javascript
// [Async with callback hell]

function requestDataA(callback) {
    // process
    getDataFromServer('urlA', function (error, responseA) {
        if (error) {
            callback(error);
        } else {
            // process responseA
            requestDataB(responseA, function (error, responseB) {
                if (error) {
                    callback(error);
                } else {
                    // process responseB
                    requestDataC(responseB, function (error, responseC) {
                        if (error) {
                            callback(error);
                        } else {
                            // process responseC
                            requestDataC(responseC, function (error, responseD) {
                                if (error) {
                                    callback(error);
                                } else {
                                    // Final processing with responseD
                                    callback(null, responseD);
                                }
                            });
                        }
                    });
                }
            });
        }
    });
}
requestDataA();

// What is the issue ?
// - in order to make sure every earlier getData "success/resolve", before getting the subsequent getData
// - the code have to be put in a fasion that will eventually become "infinite nesting" (aka "callback hell")
// - moreover, each time there's an error you will have to write a handle statement
```

#### Async with Promise 

From the following example you can see all the issue mentioned aboved getting **resolved by promise**: 

```javascript
// [ASYNC with Promise]

function requestDataA() {
    return getDataFromServerPromise('urlA');
}

function requestDataB(data) {
    return getDataFromServerPromise('urlB?data=' + data);
}

function requestDataC(data) {
    return getDataFromServerPromise('urlC?data=' + data);
}

requestDataA()
    .then(responseA => {
        return requestDataB(responseA);
    })
    .then(responseB => {
        return requestDataC(responseB);
    })
    .then(finalResponse => {
        console.log('Final data processed:', finalResponse);
    })
    .catch(error => {
        console.error('Error during requests:', error);
    });

// What problem does this resolve ?
// 1. [avoid nesting]            : promise allow you to chain the "then" method,
//                                 so each subseqeunt operation can be handled at a "higher-level" ("same-level" rather than "nesting-level")
// 2. [unified error handling]   : annd error is handled at one place in the "catch" method
// 3. [redability]               : the code is much more readable and understand, making modification/maintennance of the code much more friendly
//
// Metaphoric notation for promise ?
// - [promise maker   ] : promise eventual resolve/reject
// - [promise receiver] : receive immediate promise object from the "promise maker"
//
```



**Benifit of promise (by ColorCode)**

-   avoid the **callback hell** (or pyramid of doom)
-   **readability** of code (modifying is easier)
-   no callback **passed into the function** (the only thing passing in is the relevant argument that need to be used for the promise, say URL), hence making our function signiture a lot simplier
-   all **error handled together** (or optionally seprately see, see the ↓↓ example below ↓↓) 



```javascript
// ======================
// [Promise error handling]
//
// [Error Handling in Promise]:
// You can either:
//         - give specific error-handle function for each promise in the chain
//         - use the final "catch" block as the place where errors are resolved

let getDate;
let getCountry;
let getLocation;
let getHistoricalWeather;
let getHistoricalRaindrop;

// Error handling in one place [most recommended !]
getDate.then(
    (data)  =>{getCountry(data)},
).then(
    (data)  =>{getLocation(data)},
)
.then(
    (data)  =>{getHistoricalWeather(data)},
).then(
    (data)  =>{getHistoricalRaindrop(data)},
).catch(
    (error)=>{
        if(        error == "no [date]     data found"){
            console.log("...");
        } else if (error == "no [country]  data found"){
            console.log("...");
        } else if (error == "no [location] data found"){
            console.log("...");
        } else if (error == "no [weather]  data found"){
            console.log("...");
        } else if (error == "no [raindrop] data found"){
            console.log("...");
        }
    }
);


// Specific error handling...
getDate.then(
        (data)  =>{getCountry(data)},
        (error) =>{console.log(error);}
    ).then(
        (data)  =>{getLocation(data)},
        (error) =>{console.log(error);}
    )
    .then(
        (data)  =>{getHistoricalWeather(data)},
        (error) =>{console.log(error);}
    ).then(
        (data)  =>{getHistoricalRaindrop(data)},
        (error) =>{console.log(error);}
    );


// Error handling in a mixed manner
getDate.then(
            (data)  =>{getCountry(data)},
        ).then(
            (data)  =>{getLocation(data)},
        )
        .then(
            (data)  =>{getHistoricalWeather(data)},
            (error) =>{console.log(error);}               // ← handle error here ....
        ).then(
            (data)  =>{getHistoricalRaindrop(data)},
        ).catch(
            (error)=>{
                if(        error == "no [date]     data found"){
                    console.log("...");
                } else if (error == "no [country]  data found"){
                    console.log("...");
                } else if (error == "no [location] data found"){
                    console.log("...");
                // } else if (error == "no [weather]  data found"){  ← Don't need anymore ...
                //    console.log("...");                            ← Don't need anymore ...
                } else if (error == "no [raindrop] data found"){
                    console.log("...");
                }
            }
        );

// ======================
```















## Reference 

-   https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#:~:text=A%20Promise%20is%20a%20proxy,success%20value%20or%20failure%20reason.
-   https://www.youtube.com/watch?v=TnhCX0KkPqs



















