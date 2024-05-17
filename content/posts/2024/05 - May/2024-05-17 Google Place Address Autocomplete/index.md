---
title: "Address Input Auto-Complete (via Google Place API)"
date: "2024-05-17"
categories: ["Google Map"]
---



PENDING EXPLAINATION ....



## index.md

```html
<html>

<head>
    <title>Place Autocomplete Address Form</title>
    <script type="module" src="./index.js"></script>
    <style>
        .full-field {
            width: 400px;
            display: flex;
            justify-content: space-between;
        }

        .full-field>.form-label {
            display: block;
            text-align: left;
            margin-right: 10px;
        }

        .full-field>input {
            width: 250px;
        }
        .pac-container:after {
            background-image: none !important;
            height: 0px;
        }
    </style>
</head>

<body>
    <form id="address-form" action="" method="get" autocomplete="off">
        <label class="full-field">
            <span class="form-label">Search</span>
            <input id="search" name="search" required autocomplete="off" />
        </label>
        <br>
        <label class="full-field">
            <span class="form-label">Address1</span>
            <input id="address1" name="address1" required autocomplete="off" />
        </label>
        <br>
        <label class="full-field">
            <span class="form-label">Address2</span>
            <input id="address2" name="address2" />
        </label>
        <br>
        <label class="full-field">
            <span class="form-label">City*</span>
            <input id="locality" name="locality" required />
        </label>
        <br>
        <label class="full-field">
            <span class="form-label">State/Province*</span>
            <input id="state" name="state" required />
        </label>
        <br>
        <label class="full-field" for="postal_code">
            <span class="form-label">Postal code*</span>
            <input id="postcode" name="postcode" required />
        </label>
        <br>
        <label class="full-field">
            <span class="form-label">Country/Region*</span>
            <input id="country" name="country" required />
        </label>
    </form>

    <script
        src="https://maps.googleapis.com/maps/api/js?key=AIzaSyB0q7MRzP5phqe8r26v9qi_rEoCwFFrXck&callback=initAutocomplete&libraries=places&v=weekly"
        defer></script>
</body>

</html>
```



## index.js

```javascript

let form_search;                // field for address search
let form_address1;              // field of address 1
let form_address2;              // field of address 2
let form_city;                  // field of city
let form_stateProvince;         // field of state/province
let form_country;               // field of country
let form_postal;                // field of postal code
let gpla_autocomplete;         // auto complete object

function gpla_initAutocomplete() {
	form_search        = document.querySelector("#search");
	form_address1      = document.querySelector("#address1");
	form_address2      = document.querySelector("#address2");
    form_city          = document.querySelector("#locality");
    form_stateProvince = document.querySelector("#state");
	form_country       = document.querySelector("#country");
	form_postal        = document.querySelector("#postcode");

    // Initialize the auto-complete api and its cooresponding listener
	gpla_autocomplete  = new google.maps.places.Autocomplete(
        form_search, {
            componentRestrictions: { country: ["au", "nz"] },                         //restricting addresses in the Australia and New Zealand.
            fields:                ["name","address_components", "geometry", "icon"], //specify field needed (https://developers.google.com/maps/documentation/javascript/place-autocomplete#specify-data-fields)
            types:                 ["address"],
        }
    );
	gpla_autocomplete.addListener("place_changed", gpla_fillInAddress);
}

function gpla_fillInAddress() {
    // Initialize the values which
    // will later be filled into the fields
	let place_address1      ="";
	let place_address2      ="";
    let place_city          ="";
    let place_stateProvince ="";
    let place_country       ="";
    let place_postcode      ="";

    // `Extract address components from place details and populate corresponding form fields.
    // The place.address_components are google.maps.GeocoderAddressComponent objects. (http://goo.gle/3l5i5Mr)
	const place = gpla_autocomplete.getPlace();
	for (const component of place.address_components) {
		switch (component.types[0]) {
            case "street_number":               {place_address1      = `${component.long_name} ${place_address1}`;   break;}
			case "route":                       {place_address1      += component.short_name;                        break;}
			case "subpremise":                  {place_address2      = `${component.long_name}`;                     break;}
			case "postal_code":                 {place_postcode      = `${component.long_name}${place_postcode}`;    break;}
			case "postal_code_suffix":          {place_postcode      = `${place_postcode}-${component.long_name}`;   break;}
			case "locality":                    {place_city          = component.long_name;                          break;}
			case "administrative_area_level_1": {place_stateProvince = component.short_name;                         break;}
			case "country":                     {place_country       = component.long_name;                          break;}
		}
	}

    // Filling the retrived value from google place api
    // into the cooresponding field in the webform
	form_address1.value       = place_address1;
	form_address2.value       = place_address2;
	form_postal.value         = place_postcode;
	form_city.value           = place_city;
    form_country.value        = place_country;
    form_stateProvince.value  = place_stateProvince;
}

window.initAutocomplete = gpla_initAutocomplete;

```





## Reference

-   [Place Autocomplete - Maps JavaScript API](https://developers.google.com/maps/documentation/javascript/place-autocomplete)
-   [Place Autocomplete Address Form - Sample](https://developers.google.com/maps/documentation/javascript/examples/places-autocomplete-addressform#maps_places_autocomplete_addressform-html) ←★
-   [Place Searches on Inetractive Map - Sample](https://developers.google.com/maps/documentation/javascript/examples/place-search) 
-   [Place AutoComplete API - Guide](https://developers.google.com/maps/documentation/places/web-service/autocomplete)
-   [Place Widgets - PlaceAutocompleteElement class](https://developers.google.com/maps/documentation/javascript/reference/places-widget#Autocomplete)