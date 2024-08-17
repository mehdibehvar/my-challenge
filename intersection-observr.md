# IntersectionObserver

**The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.**

## Key Concepts:
- IntersectionObserver: The main object that tracks the visibility of an element.
- IntersectionObserverEntry: An object representing a change in the intersection between the target element and its root container at a specific moment in time.
- root: The element that is used as the viewport for checking visibility. If null, the browser viewport is used.
- rootMargin: An offset around the root that can be used to grow or shrink the area considered for intersections.
- threshold: A list of thresholds at which to trigger the observer callback. For example, a threshold of 0.5 triggers the callback when 50% of the target element is visible.

```js
    // Callback function to be executed when observer detects changes
    function onIntersection(entries, observer) {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const img = entry.target;
                img.src = img.dataset.src; // Load the image
                observer.unobserve(img); // Stop observing the image once it's loaded
            }
        });
    }

    // Create an IntersectionObserver instance
    const observer = new IntersectionObserver(onIntersection, {
        root: null, // Default is the viewport
        rootMargin: '0px',
        threshold: 0.1 // Trigger when 10% of the image is visible
    });

    // Observe each lazy-load image
    document.querySelectorAll('.lazy-load').forEach(img => {
        observer.observe(img);
    });
```
### JavaScript:

- onIntersection(entries, observer): This is the callback function that runs whenever the observer detects that an observed element's visibility changes. If an element (entry.target) is intersecting (i.e., visible), the data-src attribute is moved to src, and the image is loaded.
- observer.unobserve(img): This stops the observer from watching the image after it has been loaded, which is an optimization to prevent unnecessary checks.
- IntersectionObserver(onIntersection, options): This creates the observer. The options specify that the root is the viewport (default), there is no root margin, and the threshold is 0.1 (10% visibility).
- observer.observe(img): The observer starts observing each image with the lazy-load class.


## Benefits:
- Performance: It offloads the need to continuously poll for element visibility, which is resource-intensive.
- Ease of Use: It simplifies tasks that traditionally required complex scroll event listeners and calculations.
  
[Link](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)
