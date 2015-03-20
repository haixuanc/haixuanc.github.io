---
layout: post
title: "All About the Size"
date: 2015-03-20 20:00:00
categories:
- HTML
- CSS
- Browsers
---

## Part 1: Device Pixels vs CSS Pixels

Device pixels are the physical pixels of the display.

- Modern browsers implement zooming as "stretching up" CSS pixels. 
- Zooming in results in less CSS pixels being able to fit into the display.
- Zooming out results in more CSS pixels being able to fit into the display.

### 100% Zoom

> At **zoom level 100%** one CSS pixel is exactly equal to one device pixel.

---

## Part 2: The Widths and Heights

### Screen Size

`screen.width` and `screen.height`

- contatins teh total width and height of the user's display;
- is measured in *device pixels*;
- they never change.

### Window Size

`window.innerWidth` and `window.innerHeight`

- contains the inner width and height of the user's browser window;
- is measured in *CSS pixels*;
- includes the scrollbars for historical reasons.

If user zooms in you get less space available in the window, and `window.innerWidth` and `window.innerHeight` decrease because they are measured in CSS pixels.

### Viewport Size

`document.documentElement.clientWidth` and `document.documentElement.clientHeight`
They don't count scrollbars.

#### What is Viewport

Viewport is the element that contains the `document` object.

- Usually viewport is exactly equal to the **visible area** of browser window. But situation varies on mobile.
- The width/height of `document` object (`<html>`) is restricted by that of the viewport.

Normally, all block-level elements take 100% of the width/height of their parent. So the `<body>` is as wide as the `<html>`. And the `<html>` is as wide as the viewport. If viewport has the same dimension as the browser window, the `<body>` gets the same dimension as the browser window. Interesting thing will happen when user zooms in and the browser window is not big enough to hold the document and scrollbars show up, because at that time the viewport is not the same as the browser window, it is actually smaller than the browser window.

### `<html>` Size

`document.documentElement.offsetWidth` and `document.documentElement.offsetHeight`

- These properties truly give you access to the `<html>` element as a block-level element.
- If you set CSS property like `width`, `document.documentElement.offsetWidth` will reflect it.

---

## Part 3: The Scrolling Offset

`window.pageXOffset` and `window.pageYOffset`

- contains the horizontal and vertical scrolling offests of the `document`;
- is measured in *CSS pixels*.

If user zooms in after scrolling the page up, the browser keeps the top-left point of the `document` untouched in browser window and stretches out all CSS pixels. Therefore `window.pageXOffset` or `window.pageYOffset` does not change.

---

## Part 4: Event Coordinates

When a mouse event occurs, no less than five property pairs are exposed to give you information about where exactly it happened.

1. `pageX/Y` gives the coordinates relative to the `<html>` element in CSS pixels.
2. `clientX/Y` gives the coordinates relative to the *viewport* in CSS pixels.
3. `screenX/Y` gives the coordinates relative to the *screen* in device pixels.

---

## Part 5: Media Queries

```css
@media all and (max-width: 400px) {
	...
}
```

What width is the `max-width: 400px` measuring against? There are two relevant media queties:

- `width/height` uses the same values as `document.documentElement.clientWidth/Height`, the viewport in other words. It works in CSS pixels.
- `device-width/-height` uses the same values as `screen.width/height`, the screen in other words. It works in device pixels.

---

## References

- [A table of two viewports - part one](http://www.quirksmode.org/mobile/viewports.html)
