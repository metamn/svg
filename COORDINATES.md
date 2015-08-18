# The SVG Coordinate System

http://sarasoueidan.com/blog/svg-coordinate-systems/

## Basics

### Canvas

The area where the SVG is drawn; it's conceptually infinite in both directions (scalable)

### Viewport: `width` and `height`

* The area on the screen where the SVG is rendered. It has a finite size;
* If the viewport < canvas the SVG is clipped and the rest is not visible

### `viewBox`

The coordinate system to draw the SVG onto the screen.


### `preserveAspectRatio`**

When the `viewBox` has different a different aspect ratio than the Viewport
