---
layout: project
title: TextObserver
summary: Find and replace text on a webpage with whatever you want.
category: Library
---

`TextObserver` replaces text on a webpage with whatever you want, including text injected dynamically after initial page load.

```javascript
const badWordFilter = new TextObserver(text => text.replaceAll(/heck/gi, 'h*ck'));
```

Inspired by [`findAndReplaceDOMText`](https://github.com/padolsey/findAndReplaceDOMText), but with a different use case. Use `findAndReplaceDOMText` if you need to robustly substitute or wrap text that may span across multiple nodes a set number of times. `TextObserver` uses the [`MutationObserver`](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver) interface to keep track of changes in the DOM. Any dynamically updated content will automatically be processed in time linear to the amount of changes, not to the total amount of nodes. This enables usage on modern infinite-scrolling websites that make heavy use of AJAX like Reddit and Discord without performance degrading as more content is added.

See the [repository README](https://github.com/DanielZTing/TextObserver) for more details. Here's an example of a more advanced regex that uses capturing groups/backreferences to convert miles to kilometers:

```javascript
const unitConverter = new TextObserver(text => text.replaceAll(
    /(\d+\.?\d*) ?mi(\W|les?|$)/gi,
    (match, number) => (parseFloat(number) * 1.609).toFixed(2) + ' km'
));
```

The callback is not limited to a regular expression. Here's a more complex example that transforms everything into "mOcKiNg SpOnGeBoB" case. Useful for heated Internet discussions!

```javascript
const spongebobCase = new TextObserver(text => {
    let characters = Array.from(text);
    for (let i = 0; i < characters.length; i++) {
        if (Math.random() < 0.5) {
            if (characters[i].toUpperCase() === characters[i]) {
                characters[i] = characters[i].toLowerCase();
            } else {
                characters[i] = characters[i].toUpperCase();
            }
        }
    }
    return characters.join('');
});
```

You don't even have to necessarily modify the text at all if you're doing something like sentiment analysis on your Internet readings. The possibilities are endless!
