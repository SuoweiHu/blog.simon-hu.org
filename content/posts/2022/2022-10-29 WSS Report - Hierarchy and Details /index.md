---
title: "WSS Report - Hierarchy and Details "
date: "2022-10-29"
tags: ["Web Audit"]
---

# ⓪ - structure

## WSS Report Hierarchy
[PAST WSS Report & Template](https://drive.google.com/drive/folders/1THXhDMzNtwWmfMq8uqAd1j3hygOaJeLh)

- **PART-I **
	- Cover Page
	- Contact Details
	- Introduction
- **PART-II**
	- Lighthouse Report
		- Items:
			- Score of FCP,
			- Score of SI,
			- Score of LCP,
			- Score of TTI,
		- Recommendations and Overall Review
	- Accessibility Score
		- Items
			- Contrast
			- Navigation
			- Links
			- Aria
		- Recommendations and Overall Review
	- Best Practice
		- Items
			- Trust and Safety
			- Use HTTPS
			- Display Image with Correct Aspect ratio
			- User Experience
			- Browser errors were logged to the console
		- Recommendations and Overall Review
	- SEO (Search Engine Optimization)
		- Items
			- Content best Practice
			- Crawling and Indexing
			- Mobile Friendly
- **PART-III**
	- Summary
		- Score on each item of part-ii
			- Performance
			- Accessibility
			- Best Practice
			- SEO (Search Engine Optimization)
		- Justification
			- `<50` : Below Average
			- `>50` : Satisfactory
			- `>60` : Good
			- `>70` : Very Good
			- `>80`: Excellent
- **PART-IV**
	- Browser Timings (GTmetrix Reports)
	- Browser Timing
		- Distribution Pie-Chart
		- Scores &  Explanation of the score
			- redirection duration
			- connection duration
			- backend duration
			- time to first byte (TTFB)
			- first paint
			- dom interactive time
			- dom content load time
			- onboard time
			- fully load time
- **PART-V**
	- Security Check
		- Using SSL Certificate
		- Web Backup (statement)
- **Part-IV**
	- Conclusion
	- Attachment
		- Technical definition for lighthouse
# ⓪ - exporation & purpose

(WSS Report → Web Security Service Report)




## Terminologies
Core Web Vital Assessment :
- LCP (Largest Content-ful Paint)
- FID (First Input Delay)
- CLS (Cumulative Layout Layout Shift)

Other Notable Metrics
- FCP (First Content-ful Paint)
- INP (Interaction to Next Paint)
- TTFP (Time to First Byte)

## How is score calculated

“Score” for Different Metrics on Lighthouse8 8
(Referenced from [web.dev](https://web.dev/performance-scoring/?utm_source=lighthouse&utm_medium=lr))
- First gather the lot of perfjoamcne metrics (mostly reported in milliseconds)
- Then converts each raw metric value into a metric score from 0 to 100 by looking at where the metric value falls on its Lighthouse scoring distribution.

Example
![](DraggedImage.png)
![](CleanShot%202022-10-20%20at%2015.42.46.png)

“Weighting” for Different Metrics on Lighthouse 8
(Referenced from [web.dev](https://web.dev/performance-scoring/?utm_source=lighthouse&utm_medium=lr))
- 10% - FCP - First Contentful Paint
- 10% - SI  - Speed Index
- 25% - LCP - Largest Contentful Paint
- 10% - TI  - Time to Interactive
- 30% - TBT - Total Blocking Time
- 15% - CLS - Cumulative Layout Shift

(The weightings are chosen to provide a balanced representation of the user's perception of performance. The weightings have changed over time because the Lighthouse team is regularly doing research and gathering feedback to understand what has the biggest impact on user-perceived performance.)

Example
![](CleanShot%202022-10-20%20at%2015.43.05.png)

### Lighthouse Scoring Calculator
[https://googlechrome.github.io/lighthouse/scorecalc/#FCP=3200&SI=4187&FMP=2010&TTI=7948&FCI=6500&LCP=2160&TBT=1705&CLS=0.02&device=mobile&version=9](https://googlechrome.github.io/lighthouse/scorecalc/#FCP=3200&SI=4187&FMP=2010&TTI=7948&FCI=6500&LCP=2160&TBT=1705&CLS=0.02&device=mobile&version=9)
![](CleanShot%202022-10-20%20at%2015.49.38.png)

# Speed Index (SI)


Speed index is one of six metrics tracked in the perofmacne section of lighthouse report. Each metrics captures some aspects of page load speed

Lighthouse displays speed-index in unit of seconds

What does speed index measures
- speed index measures how equally content is visually displayed during page load
- light house first captures a video of the page loading in the browser and the computes the visual progression between frames
- lighthouse then uses the speed line nodeJS module to generate the Speed Index score


Speed index interpretation
- 0–3.4	Green (fast)
- 3.4–5.8	Orange (moderate)
- Over 5.8	Red (slow)

Improving on speed index
![](CleanShot%202022-10-20%20at%2016.01.44.png)

# First Contentful Paint (FCP)



First contetnful paint is one of the six metrics tracked in the performance section of the lighthouse report. Each metrics captures some aspect of page load speed

Lighthouse displays FCP in unit of secons
![](CleanShot%202022-10-20%20at%2015.54.06.png)

What FCP measures ?
- FCP measures how long it takes the browser to render the first piece of DOM content after a user navigates to your page. Image, non-white `<canvas>` elements, and SVSs on your page are considered DOM content; Anything inside an `iframe` is not included.

How to interpret the FCP time levels ?
1. `0-1.8` seconds, Green (fast) colour-coding
2. `1.8-3` seconds, Orange (moderate) colour-coding
3. `over 3` seconds, Red (slow) colour-coding

Improving FCP
![](CleanShot%202022-10-20%20at%2016.02.06.png)




# Speed Index (SI)


Speed index is one of six metrics tracked in the perofmacne section of lighthouse report. Each metrics captures some aspects of page load speed

Lighthouse displays speed-index in unit of seconds

What does speed index measures
- speed index measures how equally content is visually displayed during page load
- light house first captures a video of the page loading in the browser and the computes the visual progression between frames
- lighthouse then uses the speed line nodeJS module to generate the Speed Index score


Speed index interpretation
- 0–3.4	Green (fast)
- 3.4–5.8	Orange (moderate)
- Over 5.8	Red (slow)

Improving on speed index
![](CleanShot%202022-10-20%20at%2016.01.44-1.png)

# First Contentful Paint (FCP)



First contetnful paint is one of the six metrics tracked in the performance section of the lighthouse report. Each metrics captures some aspect of page load speed

Lighthouse displays FCP in unit of secons
![](CleanShot%202022-10-20%20at%2015.54.06-1.png)

What FCP measures ?
- FCP measures how long it takes the browser to render the first piece of DOM content after a user navigates to your page. Image, non-white `<canvas>` elements, and SVSs on your page are considered DOM content; Anything inside an `iframe` is not included.

How to interpret the FCP time levels ?
1. `0-1.8` seconds, Green (fast) colour-coding
2. `1.8-3` seconds, Orange (moderate) colour-coding
3. `over 3` seconds, Red (slow) colour-coding

Improving FCP
![](CleanShot%202022-10-20%20at%2016.02.06-1.png)

## ① - operation for SharePoint


1. Enter the WSS folder as your normally do
2. Create new folder for the following:
	1. The month where the WSS check commences
	2. The folder for the broken link
3. Copy each of the document from last month to this month, and start / testing / modifying from the top of that copied file
## ② - was step-by-step run down


1. **Contact Details **
	1. CHANGE DATE ![](CleanShot%202022-10-26%20at%2010.42.27@2x.png)

---- ------------------------------------------------------------------

(Run light house to check for the scores)

---- ------------------------------------------------------------------

2. **Website Performance Check **
	1. LIGHTHOUSE REPORT ![](CleanShot%202022-10-26%20at%2010.42.27@2x-1.png)![](CleanShot%202022-10-26%20at%2010.43.37@2x.png)
	2. CHANGING STATS ![](CleanShot%202022-10-26%20at%2010.46.13@2x.png)
	3. CHANGING VALUES ![](CleanShot%202022-10-26%20at%2010.51.02@2x.png)
	4. CHANGING STATEMENT ![](CleanShot%202022-10-26%20at%2010.52.01@2x.png)![](CleanShot%202022-10-26%20at%2010.52.56@2x.png)

3. **Website Accessibility Check**
	1. Change the item ![](CleanShot%202022-10-26%20at%2011.12.07@2x.png)![](CleanShot%202022-10-26%20at%2011.12.07@2x-1.png)

4. **Best Practice**
	1. No need to modifications if no changes
	2. If there is solved/popping stuff remove/add it

5. **SEO** (Search Engine Optimisation)
	1. No need to modifications if no changes
	2. If there is solved/popping stuff remove/add it ![](CleanShot%202022-10-26%20at%2013.34.26.png)

---- ------------------------------------------------------------------

6. **Summary**
	1. Update the scores for each of the above based on ![](CleanShot%202022-10-26%20at%2011.16.48@2x.png)

---- ------------------------------------------------------------------

7. **Browser Timings **
	1. Run GTmetric, to get the scores ![](CleanShot%202022-10-26%20at%2013.36.18.png)![](CleanShot%202022-10-26%20at%2013.36.25.png)
	2. Remember to change the technical term into non-expertise understandable language next time ![](CleanShot%202022-10-26%20at%2011.19.12@2x.png) ![](CleanShot%202022-10-26%20at%2011.19.21@2x.png)

---- ------------------------------------------------------------------

9. **SSL Security Check**
	1. Run safari, and click on the little lock icon ![](CleanShot%202022-10-26%20at%2011.22.09@2x.png)![](CleanShot%202022-10-26%20at%2011.22.41@2x.png)
	2. Then take a screenshot of the presented SSL certificate
## ③ - operation for “failed link check”



By utilising the website:
-  “[https://www.deadlinkchecker.com/](https://www.deadlinkchecker.com/)”
	![](CleanShot%202022-10-26%20at%2011.26.20@2x.png)

Step
1. Open the `deadlinkchecker`
2. Enter the url on the address bar & enter the code
3. Choose `check whole website` and click start
4. Wait for it to finish ![](CleanShot%202022-10-26%20at%2013.45.50@2x.png)
5. While you are waiting, open the `document` and `double click` on the table to open it for edit ![](CleanShot%202022-10-26%20at%2011.29.20@2x.png)
6. As you are done, copy past them into the excel ![](CleanShot%202022-10-26%20at%2011.29.20@2x-1.png)
7. Click on save (for multiple times) in excel
8. Close excel and correct formatting manually
## ④ - marking your time entries


1. Open the corresponding client’s ticket you finished ![](CleanShot%202022-10-26%20at%2011.33.32@2x.png)
2. Click on the time tab to enter time entry ![](CleanShot%202022-10-26%20at%2011.33.49@2x.png)
3. Enter note for what you did ![](CleanShot%202022-10-26%20at%2011.34.32@2x.png), for instance:
		Finished reporting for website:
		- COMPANY: XXXXYYYYZZZZZ
		- URL: www.XXXXYYYYZZZZZ.com.au
		- REPORT: WSS Report, Missing Link Report.
4. Add the note under the internal ![](CleanShot%202022-10-26%20at%2011.35.01@2x.png)
5. . Remove the send email notification item
	1. To client  ![](CleanShot%202022-10-26%20at%2011.34.32@2x-1.png)
	2. To Anil     ![](CleanShot%202022-10-26%20at%2011.34.32@2x-2.png)
6. Save the ticket time entry
# V8 Lighthouse Info


## How to improve your overall Performance score
![](DraggedImage-1.png)
[https://web.dev/first-contentful-paint/](https://web.dev/first-contentful-paint/)



#### LV8 ighthouse CLI
Official Google Lighthouse documentation
	https://developer.chrome.com/docs/lighthouse/overview/#psi

You can run the report via
	 lighthouse "https://www.google.com" --output json --output-path "google.json"

And the report will be saved to the accordingly position, and you can view the result via the website:
	https://googlechrome.github.io/lighthouse/viewer/

My Code
	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: ahl                 \n\n";  sleep 2;
	lighthouse  "https://www.ahl.gov.au"                                           --output json --output-path "01_ahl.json"                 ; sleep 2;
	printf "EXPORTING: ahl                 DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: anu                 \n\n";  sleep 2;
	lighthouse  "https://www.anu-sport.com.au"                                     --output json --output-path "02_anu.json"                 ; sleep 2;
	printf "EXPORTING: anu                 DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: btaa                \n\n";  sleep 2;
	lighthouse  "https://www.btaa.org.au"                                          --output json --output-path "03_btaa.json"                ; sleep 2;
	printf "EXPORTING: btaa                DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: calc                \n\n";  sleep 2;
	lighthouse  "https://www.calc.ngo"                                             --output json --output-path "04_calc.json"                ; sleep 2;
	printf "EXPORTING: calc                DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: crcna               \n\n";  sleep 2;
	lighthouse  "https://www.crcna.com.au"                                         --output json --output-path "05_crcna.json"               ; sleep 2;
	printf "EXPORTING: crcna               DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: homefinders         \n\n";  sleep 2;
	lighthouse  "https://www.homefinders.net.au"                                   --output json --output-path "06_homefinders.json"         ; sleep 2;
	printf "EXPORTING: homefinders         DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: legalaidact         \n\n";  sleep 2;
	lighthouse  "https://www.legalaidact.org.au"                                   --output json --output-path "07_legalaidact.json"         ; sleep 2;
	printf "EXPORTING: legalaidact         DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: embracementalhealth \n\n";  sleep 2;
	lighthouse  "https://www.embracementalhealth.org.au"                           --output json --output-path "08_embracementalhealth.json" ; sleep 2;
	printf "EXPORTING: embracementalhealth DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: asbfeo              \n\n";  sleep 2;
	lighthouse  "https://www.asbfeo.gov.au/"                                       --output json --output-path "09_asbfeo.json"              ; sleep 2;
	printf "EXPORTING: asbfeo              DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: truck               \n\n";  sleep 2;
	lighthouse  "https://www.truck.net.au/public/australian-trucking-association"  --output json --output-path "10_truck.json"               ; sleep 2;
	printf "EXPORTING: truck               DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

	printf "█████████████████████████████████████████████████████████████████████████████████████████\n EXPORTING: latrobe             \n\n";  sleep 2;
	lighthouse  "https://www.latrobe.vic.gov.au/"                                  --output json --output-path "11_latrobe.json"             ; sleep 2;
	printf "EXPORTING: latrobe             DONE!\n █████████████████████████████████████████████████████████████████████████████████████████"; sleep 2;

