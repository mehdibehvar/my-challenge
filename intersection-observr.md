# IntersectionObserver

**The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.**

*1. ساختار IntersectionObserver*

- یک callback که هر بار که عنصر مشاهده شده وارد یا خارج از viewport شود، فراخوانی می‌شود.
- گزینه‌هایی که مشخص می‌کنند که چه زمانی این callback باید اجرا شود.


!Image

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
