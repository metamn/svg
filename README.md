# SVG

Learning & playing with SVG.

## Features

https://en.wikipedia.org/wiki/Scalable_Vector_Graphics

* [Responsive](#responsive)
* [Structure](#structure)
* [Styling](#styling)
* [Animation](#animation)
* Interactive
  * Focus
  * Click
  * Scroll
  * Zoom
* Compression
* Printable
* Scripting
* Metadata


## Tools

* http://mondrian.io - Browser based SVG creator


## Usage

https://css-tricks.com/using-svg/


* `img` &mdash; No CSS control; no JS animations
* `svg` (inline) &mdash; Full CSS control; it's hard to cache
* `object` &mdash; Cannot be styled with external CSS, only internally inside the SVG file
* `data-uri` &mdash;

It seems the best usage is the inline `svg` method.
Below we will discuss only this method.



## Responsive

Let's say we have an SVG with a single 500x500px rectangle and padding top, padding left set to 100px.
This gives us a 700x700px image.

#### Fluid

To make it fluid we will have to do nothing else than:
```
<svg viewBox="0 0 700 700">
  <rect x="100" y="100" width="500.00000000000017" height="500.0000000000006"  fill="rgba(95, 205, 167, 1)" stroke="rgba(0, 0, 0, 1)" stroke-width="1"/>
</svg>
```

<p data-height="268" data-theme-id="0" data-slug-hash="mJYZJL" data-default-tab="result" data-user="metamn" class='codepen'>See the Pen <a href='http://codepen.io/metamn/pen/mJYZJL/'>Simple fluid SVG</a> by metamn (<a href='http://codepen.io/metamn'>@metamn</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

This will display the svg of dimensions set by the screen's width.  
If the screen is 320px width then the svg will be displayed on a 320x320 area.  
If the screen is 1920px width then the svg will be displayed on a 1920x1920 area.  
And the green rectangle inside will be scaled up / down depending on the screen size.

#### Full screen
```
article.fullscreen {
  height: 100vh;
  overflow: hidden;
}

article.fullscreen svg {
  width: 100%;
  height: 100%;
}
```

<p data-height="268" data-theme-id="0" data-slug-hash="QbRXML" data-default-tab="result" data-user="metamn" class='codepen'>See the Pen <a href='http://codepen.io/metamn/pen/QbRXML/'>Full screen, responsive SVG</a> by metamn (<a href='http://codepen.io/metamn'>@metamn</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>







## Structure

http://tympanus.net/codrops/2015/07/16/styling-svg-use-content-css/


### Group (`<g>`)

* Group together objects (like a layer in PSD)
* Elements inside the group are styled uniformly
* During animation elements inside a group preserve their positioning

### Definitions (`<defs>`)

* To store reusable elements
* `defs` are not rendered until they are instantiated via a call
* They are useful to define patterns like gradients

### Symbols (`<symbol>`)

* Combine `<g>` and `<defs>` together
* They don't define patterns but ore complex objects
* It's responsive via `viewBox`

### Use (`<use>`)

* Renders a previously defined `<g>`, `<defs>` or `<symbol>`
* `<g>`, `<defs>` and `<symbol>` are stored in the __Shadow DOM__. `<use>` creates and instance of them in the DOM.
* Every `<use>` can be styled separately like objects in OOP

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
* If we want to set other attributes we have to use custom CSS variables

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



## Animation


https://css-tricks.com/weighing-svg-animation-techniques-benchmarks/


* There are 3 ways to animate SVG:
  * Standard CSS animations and transitions
  * Javascript animations
  * Native (SMIL) animations

### CSS

* SVG animations can be similar to CSS animations and transitions via by their nature. Keyframes are created, things move, colors change, etc.
* Any transformation or transition animation that can be applied to an HTML element can also be applied to an SVG element
* Since not all SVG (presentation) attributes are accessible by CSS, standard animations are available only for a subset of the SVG properties.

### Javascript

* With tools like http://snapsvg.io/, https://github.com/julianshapiro/velocity, https://github.com/greensock/GreenSock-JS/
* They don't work with `img` and `background-image`

### SMIL

* SMIL seems to be a complete, very powerful animation framework like the best others out there (GreenSock)
* It seems to have the best performance among all

More details in [SMIL.md](SMIL.md)

#### Which one to use and when

* CSS &mdash; For small small transitions or simple animations like hover etc.
* SMIL &mdash; For morphing elements, physics and more.
* Velocity.js &mdash; hmm
* GSAP &mdash; For very complex animations
