# SMIL Animations

https://css-tricks.com/guide-svg-animations-smil/

### Basics

* You can animate one attribute at a time through `attributeName`.
* If there are more animations a new `<animate>` has to be created for each of them
* Animations are chainable via the `begin` parameter

```
<circle id="orange-circle" r="30" cx="50" cy="50" fill="orange" />

<rect id="blue-rectangle" width="50" height="50" x="25" y="200" fill="#0099cc"></rect>

  <animate
    xlink:href="#orange-circle"
    attributeName="cx"
    from="50"
    to="450"
    dur="5s"
    begin="click"
    fill="freeze"
    d="circ-anim" />

  <animate
    xlink:href="#blue-rectangle"
    attributeName="x"
    from="50"
    to="425"
    dur="5s"
    begin="circ-anim.begin + 1s"
    fill="freeze"
    id="rect-anim" />
```

### Keyframes

* As in CSS the animation can follow a special rhythm using the `keyTimes` and `values` parameters

```
<animate
    xlink:href="#orange-circle"
    attributeName="cx"
    from="50"
    to="450"
    dur="2s"
    begin="click"
    values="50; 490; 350; 450"
    keyTimes="0; 0.5; 0.8; 1"
    fill="freeze"
    id="circ-anim" />
```

* With `keyLines` an easing function can be added like cubic-bezier


### Loops

* The `begin` and `end` parameters can be lists. This makes the animation to be repeated on certain intervals


### Morphing / Shape Tweening

http://codepen.io/noahblon/blog/an-intro-to-svg-animation-with-smil

* Unlike CSS, SVG shapes can be animated to morph into another shape
* The data from `d` (vertices/points) has to be moved inside the animation into the `values` attribute
* In order to be able to morph shapes, the start, end, and any intermediate path shapes need to have the exact same number of vertices/points, and they need to appear in the same order. If the number of vertices doesn't match, the animation wouldn't work.

```
<svg viewbox="0 0 100 100">
  <path fill="#1EB287">
    <animate
             attributeName="d"
             dur="3000ms"
             repeatCount="indefinite"
             values="M 0,0
                     C 50,0 50,0 100,0
                     100,50 100,50 100,100
                     50,100 50,100 0,100
                     0,50 0,50 0,0
                     Z;

                     M 25,50
                     C 37.5,25 37.5,25 50,0
                     75,50 75,50 100,100
                     50,100 50,100 0,100
                     12.5,75 12.5,75 25,50
                     Z;"/>
  </path>
</svg>
```

### Animation along arbitrary paths (`animateMotion`, `mpath`, `rotate`)

* Animates an object along a line, circle, or any path
* The path can be part of the `animation` element or can be an external element referenced by `mpath`
* With `rotate` the animated element can follow the path in a natural way. If the object is on the downside of the path it will be rotated down. And so on

See demo at http://codepen.io/SaraSoueidan/pen/48caf2f5fa42a8c154fcb5dec0dbe4d5

### Animating text along a path (`textPath`)

* It is not done by `animateMotion` but `animate` and using `text` element's `textPath` attribute

### Transformations (`animateTransform`)

* Supports transformations like `translate`, `scale`, `rotate`, `skew`
* To use one first must understand the [SVG coordinate system](COORDINATES.md)  
especially what is the `viewBox`, `viewport` and the `preserveAspectRatio`
