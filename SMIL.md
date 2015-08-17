# SMIL animations

https://css-tricks.com/guide-svg-animations-smil/

### Basics

* you can animate one attribute at a time through `attributeName`.
* if there are more animations a new `<animate>` has to be created for each of them
* animations are chainable via the `begin` parameter

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
