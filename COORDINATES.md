# The SVG Coordinate System

http://sarasoueidan.com/blog/svg-coordinate-systems/

## Basics

* **Canvas** &mdash; The area where the SVG is drawn; it's conceptually infinite in both directions (scalable)
* **Viewport: `width` and `height`** &mdash; The area on the screen where the SVG is rendered. It has a finite size; if the viewport < canvas the SVG is clipped and the rest is not visible
* **`viewBox`** &mdash; The coordinate system to draw the SVG onto the screen.
* **`preserveAspectRatio`** &mdash; When the `viewBox` has different a different aspect ration than the Viewport
