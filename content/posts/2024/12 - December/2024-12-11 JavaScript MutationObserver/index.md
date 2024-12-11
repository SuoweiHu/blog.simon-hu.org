---
title: "JavaScript MutationObserver [PENDING]"
date: "2024-12-11"
categories: ["JavaScript"]
---

MutationObserver
- https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver
- https://hacks.mozilla.org/2012/05/dom-mutationobserver-reacting-to-dom-changes-without-killing-browser-performance/
- https://codepen.io/milofultz/pen/LYjPXPw




Example
- https://nginx-feature-phase1-migrated-new-chiefscientist.govcms7.amazee.io/news/publications
```javascript
// REMOVE TRAILING SPACE FOR AUTO COMPLETE ON PUBLICATION AND SPEECHES
    function addEventListener_removeAutoCompleteNumber(input_selector) {
      const removeTrailingNumberPattern = (str) => str.replace(/\s*\(\d+\)$/, '');

      const attachHandlers = (input) => {
          const updateValue = () => {
              setTimeout(() => {
                  input.value = removeTrailingNumberPattern(input.value);
              }, 0);
          };

          // Handle focusout for manual cleanup
          input.addEventListener('focusout', () => {
              input.value = removeTrailingNumberPattern(input.value);
          });

          // Handle dynamic autocomplete menu updates
          const observer = new MutationObserver((mutations) => {
              mutations.forEach((mutation) => {
                  if (mutation.addedNodes.length) {
                      document.querySelectorAll("ul.ui-menu.ui-autocomplete > li > a.ui-menu-item-wrapper").forEach((item) => {
                          item.onclick = () => updateValue();
                      });
                  }
              });
          });

          // Observe the autocomplete menu for changes
          const autocompleteMenu = document.querySelector(".ui-menu.ui-autocomplete");
          if (autocompleteMenu) {
              observer.observe(autocompleteMenu, { childList: true });
          }
      };

      // Attach handlers to all matching inputs
      document.querySelectorAll(input_selector).forEach((input) => {
          input.addEventListener('input', () => {
              setTimeout(() => attachHandlers(input), 500);
          });
      });
    }

    // Initialize on DOM load
    document.addEventListener('DOMContentLoaded', () => {
      addEventListener_removeAutoCompleteNumber(".path-news input[data-once='autocomplete']");
      addEventListener_removeAutoCompleteNumber(".path-speeches input[data-once='autocomplete']");
      addEventListener_removeAutoCompleteNumber(".path-publications input[data-once='autocomplete']");
    });
```