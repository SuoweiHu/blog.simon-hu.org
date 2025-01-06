---
title: "Explaining Tone Curve Tool (via bottom-left anchor)"
date: "2024-12-17"
tags: ["Photography"]
---



## RGB Tone Curve 

### Movement for Bottom-left Anchor  

-   **RIGHT**

    -   When you move the bottom-left anchor of the RGB tone curve right

        -   you are **clipping the shadow** of the original image (on the left of the anchor)

            (i.e. you are making a portion of the shadow in the image to become completly black)

        -   you are **increasing the brightness midtone and highlight**  (or increasing contrast) of the original image

            (i.e. you are mapping the remaining luminance range from the right of the anchor to 100% to the 0%~100% range )

-   **UP**

    -   When you move the bottom-left anchor of the RGB tone curve up

        -   you are turning the **black into gray** 

            (that's how people add the film look sometimes, but we can do the opposite by moving it right)

        -   you are **increasing the brightness for shadow, midtone, highlight** 

-   **BOTH**
    -   When you move the bottom-left anchor of the RGB tone curve both up and right 
        -   you are **clipping a portion of the shadow** and **turning this portion of the shadow along with black into gray**
        -   right-of-anchor
            -   if point above diagonal line: **increasing the brightness** 
            -   if point below diagonal line: **reducing the brightness**
            -   if point on the diagonal line: **retaining the original contrast** (luminance to the right of anchor uneffected)

-   **ILLUSTRATION** 

    ![2024-12-19T000303](2024-12-19T000303.png)





---

## Red Tone Curve

### Movement for Bottom-left Anchor 

-   **RIGHT**
    -   When you move the bottom-left anchor of the Redtone curve right  
        -   **adding cyan** (to the whole image, aka: black+midtone+highlight)
        -   **removing red**   (same)
-   **UP** 
    -   When you move the bottom-left anchor of the Red tone curve up
        -   **adding red**   (same)
        -   **removing cyan**   (same)

-   **BOTH**
    -   When you do a combination of both up and right
        -   making a **portion of the shadow become completely red**
        -   luminance range on the right of the anchor
            -   if point above diagonal line: **add red to image** 
            -   if point below diagonal line: **add cyan to image**
            -   if point on the diagonal line: **retaining the original color** 

-   **ILLUSTRATION**

    ![2024-12-19T002344](2024-12-19T002344.png)



---

## Green Tone Curve

### Movement for Bottom-left Anchor 

-   **RIGHT**
    -   When you move the bottom-left anchor of the Green/Purple tone curve right  
        -   **adding purple**  (to the whole image, aka: black+midtone+highlight)
        -   **removing green**  (same)

-   **UP**

    -   When you move the bottom-left anchor of the Green tone curve up

        -   **adding green**  (same)

        -   **removing purple**  (same)

-   **BOTH**
    -   When you do a combination of both up and right
        -   making a **portion of the shadow become completely green**
        -   luminance range on the right of the anchor
            -   if point above diagonal line: **add green to image** 
            -   if point below diagonal line: **add purple to image**
            -   if point on the diagonal line: **retaining the original color** 

-   **ILLUSTRATION**

    ![2024-12-19T002219](2024-12-19T002219.png)



---

## Blue Tone Curve

### Movement for Bottom-left Anchor 

-  **RIGHT**
    -   When you move the bottom-left anchor of the Blue tone curve right  
        -   **adding yellow** (to the whole image, aka: black+midtone+highlight)
        -   **removing blue**  (same)

- **UP**

    - When you move the bottom-left anchor of the Blue tone curve up

        - **adding blue**  (same)

        -   **removing yellow** (same)

-   **BOTH**
    -   When you do a combination of both up and right
        -   making a **portion of the shadow become completely blue**
        -   luminance range on the right of the anchor
            -   if point above diagonal line: **add blue to image** 
            -   if point below diagonal line: **add yellow to image**
            -   if point on the diagonal line: **retaining the original color** 

-   **ILLUSTRATION**

    ![2024-12-19T002524](2024-12-19T002524.png)
