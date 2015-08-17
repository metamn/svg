# SVG

Learning & playing with SVG.

## Features

https://en.wikipedia.org/wiki/Scalable_Vector_Graphics

* styleable
* responsive
* animatable
* compressible
* printable
* interactive
  * focus
  * click
  * scroll
  * zoom
* scriptable
* metadata


## Tools

* http://mondrian.io - browser based SVG creator


## Usage

https://css-tricks.com/using-svg/


* `img` &mdash; no CSS control
* `svg` (inline) &mdash; full CSS control; it's hard to cache
* `object` &mdash; cannot be styled with external CSS, only internally inside the svg file
* data-uri &mdash;


## Responsive

http://demosthenes.info/blog/744/Make-SVG-Responsive

http://tympanus.net/codrops/2014/08/19/making-svgs-responsive-with-css/

* `img`: `<img src="monkey.svg" alt="Monkey face" style="width: 100%; height: auto;">`
* `svg`: is responsive by default
* `object`: complicated

New browser make `svg` and `img` responsive by default. The condition is to have SVG attributes all stripped down to basics.

The Mondrian generated SVG file:
```
<!-- Made in Mondrian.io -->
<svg xmlns:mondrian="http://mondrian.io/xml" xmlns="http://www.w3.org/2000/svg" version="1.1" height="800" width="1000" id="main" style="width: 1000px; height: 800px; transform: scale(1);" viewbox="0 0 1000 800" enable-background="new 0 0 1000 800">
<ellipse cx="273" cy="261.5" rx="94" ry="92.5"  fill="rgba(95, 205, 167, 1)" stroke="rgba(0, 0, 0, 1)" stroke-width="1"/>
<path stroke="rgba(0, 0, 0, 1)" fill="rgba(95, 205, 167, 1)" stroke-width="1" d="M106,111 L628,495" />
</svg>
```

The resposnive version:
```
<svg version="1.1" viewbox="0 0 1000 800">
  <ellipse cx="273" cy="261.5" rx="94" ry="92.5"  fill="rgba(95, 205, 167, 1)" stroke="rgba(0, 0, 0, 1)" stroke-width="1"/>
  <path stroke="rgba(0, 0, 0, 1)" fill="rgba(95, 205, 167, 1)" stroke-width="1" d="M106,111 L628,495" />
</svg>
```

Older browsers like IE needs hacks presented in the above articles.





## Structure

http://tympanus.net/codrops/2015/07/16/styling-svg-use-content-css/


### Group (`<g>`)

* group together objects (like a layer in PSD)
* elements inside the group are styled uniformly
* during animation elements inside a group preserve their positioning

### Definitions (`<defs>`)

* to store reusable elements
* `defs` are not rendered until they are instantiated via a call
* they are useful to define patterns like gradients

### Symbols (`<symbol>`)

* combine `<g>` and `<defs>` together
* they don't define patterns but ore complex objects
* it's responsive via `viewBox`

### Use (`<use>`)

* renders a previously defined `<g>`, `<defs>` or `<symbol>`
* `<g>`, `<defs>` and `<symbol>` are stored in the __Shadow DOM__. `<use>` creates and instance of them in the DOM.
* every `<use>` can be styled separately like objects in OOP

```
<svg>
  <symbol id="ic">
    <path fill="#000" d="M81,40.933c0-4.25-3-7.811-6.996-8.673c-0.922-5.312-3.588-10.178-7.623-13.844  c-2.459-2.239-5.326-3.913-8.408-4.981c-0.797-3.676-4.066-6.437-7.979-6.437c-3.908,0-7.184,2.764-7.979,6.442  c-3.078,1.065-5.939,2.741-8.396,4.977c-4.035,3.666-6.701,8.531-7.623,13.844C22.002,33.123,19,36.682,19,40.933  c0,2.617,1.145,4.965,2.957,6.589c0.047,0.195,0.119,0.389,0.225,0.568l26.004,43.873c0.383,0.646,1.072,1.04,1.824,1.04  c0.748,0,1.439-0.395,1.824-1.04L77.82,48.089c0.105-0.179,0.178-0.373,0.225-0.568C79.855,45.897,81,43.549,81,40.933z   M49.994,11.235c2.164,0,3.928,1.762,3.928,3.93c0,2.165-1.764,3.929-3.928,3.929s-3.928-1.764-3.928-3.929  C46.066,12.997,47.83,11.235,49.994,11.235z M27.842,36.301c0.014,0,0.027,0,0.031,0c1.086,0,1.998-0.817,2.115-1.907  c0.762-7.592,5.641-13.791,12.303-16.535c1.119,3.184,4.146,5.475,7.703,5.475c3.561,0,6.588-2.293,7.707-5.48  c6.664,2.742,11.547,8.944,12.312,16.54c0.115,1.092,1.037,1.929,2.143,1.907c2.541,0.013,4.604,2.087,4.604,4.631  c0,1.684-0.914,3.148-2.266,3.958H25.508c-1.354-0.809-2.268-2.273-2.268-3.958C23.24,38.389,25.303,36.316,27.842,36.301z   M50.01,86.723L27.73,49.13h44.541L50.01,86.723z"/>
  </symbol>
</svg>

<svg class="icon" viewBox="0 0 100 125">
    <use class="ic-1" xlink:href="#ic" x="0" y="0" />
</svg>

<svg class="icon" viewBox="0 0 100 125">
    <use class="ic-2" xlink:href="#ic" x="0" y="0" />
</svg>

use.ic-1 {
    // CSS here;
}

use.ic-2 {
    // CSS here;
}
```

Even if the first `<svg>` is just a declaration (belongs to Shadow DOM) the browser will render an empty 300x150px area.
Hence all declarations must have set `display: none`



## Style

* Presentation attributes &mdash; SVG has special styling like `stroke`, `fill` etc.
* SVG can be styled with CSS
* Some of these style attributes are shared (`<opacity`, `<transform>`) and some are not

### Style overwriting (`inherit`)

CSS can overwrite SVG presentation attributes:

```
use.ic-1 {
    fill: skyblue;
}

use.ic-2 {
    fill: #FDC646;
}

svg path {
    fill: inherit;
}
```

Without the `svg path ... inherit` declaration the original SVG color `#000` wouldn't be overwritten


### Style overwriting (`all`)

```
svg path {
    all: inherit;
}
```

This will make all SVG attributes which are controllable via CSS to be overwritten


### Style overwriting (`currentColor`)

```
<svg style="display: none;">
	<symbol id="codrops" viewBox="0 0 23 30">
		<path class="back" d="..."/>
		<path class="front" fill="currentColor" d="..."/>
	</symbol>
</svg>

<svg height="90px" width="69px">
  <use xlink:href="#codrops" class="codrops-1"/>
</svg>
<svg height="90px" width="69px">
  <use xlink:href="#codrops" class="codrops-2"/>
</svg>

.codrops-1 {
  fill: #4BC0A5;
  color: #A4DFD1;
}
.codrops-2 {
  fill: #0099CC;
  color: #7FCBE5;
}
```

* `path.back` will be coloured by `color`
* `path.front` will be coloured by `fill`


### Style overwriting with CSS Custom Properties a.k.a CSS Variables

* `currentColor` is the only CSS variable available in SVG today.
* if we want to set other attributes we have to use custom CSS variables

```
<svg style="display: none">
    <symbol id="robot" viewBox="0 0 340 536">
        <path d="..." fill="#fff" />
        <path d="..." fill="#D1312C" />
        <path d="..." fill="#1E8F90" style="fill: var(--primary-color, #1E8F90)" />
        <path d="..." fill="#1E8F90" style="fill: var(--primary-color, #1E8F90)" />
        <path d="..." fill="#fff" />
        <path d="..." fill="#6A4933" style="fill: var(--tertiary-color, #6A4933)" />
        <path d="..." fill="#1E8F90" style="fill: var(--primary-color, #1E8F90)" />
        <path d="..." fill="#6A4933" style="fill: var(--tertiary-color, #6A4933)" />
        <path d="..." fill="#fff" />
        <path d="..." fill="#6A4933" style="fill: var(--tertiary-color, #6A4933)" />
        <path d="..." fill="#F2B42B" style="fill: var(--secondary-color, #F2B42B)" />
        <path d="..." fill="#fff" />

         <!-- rest of the shapes -->
    </symbol>
</svg>

<svg width="340" height="536">
    <use xlink:href="#robot" id="robot-1" />
</svg>

#robot-1 {
  --primary-color: #0099CC;
  --secondary-color: #FFDF34;
  --tertiary-color: #333;
}
```

`var(--primary-color, #1E8F90)` is a custom CSS variable with a fallback color (`#1E8F90`).

Currently only Firefox supports CSS variables. http://caniuse.com/#feat=css-variables
