Pixelate
========

>Build status:  | &nbsp;
>---------------|------------------------------------------------------------
>Master         | [![Build Status][travis-image-master]][travis-url-master]
>In development | [![Build Status][travis-image-develop]][travis-url-develop]

Pixelate an image's canvas just by select.

Overview
========

This libray can turn an image's canvas to a selectable area that you can select and real time
preview what is changing.

Here are the sample of what this pixelate library can do:

![State 1](https://code.teracy.org/projects/PILOT/repos/pixelate/browse/app/assets/state-1.png?raw)
![State 2](https://code.teracy.org/projects/PILOT/repos/pixelate/browse/app/assets/state-2.png?raw)


Checkout this demo for a closer look: http://teracy-official.github.io/pixelate/

Usage
=====

```js
var canvas = document.createElement('canvas'),
    context,
    img = new Image();

img.onload = function() {
    context = canvas.getContext('2d');
    canvas.width = img.width;
    canvas.height = img.height;
    context.drawImage(img, 0, 0);
    var pxl = pixelate(canvas, {
                radius: 10,
                selector: {
                  masked: true, // mask on select
                  strokeStyle: 'black'
                }
            });
    pxl.select(0, 0, 50, 50);
};
img.src = 'images/sample.png';
```

APIs
=====

select(x, y, width, height)
---------------------------

Selects an area for masking, unmasking and pixelating.

**Example usage**:

```js
var pxl = pixelate(canvas);
pxl.select(0, 0, 50, 50);
```

clear()
-------

Clears the selected area.

**Example usage**:

```js
var pxl = pixelate(canvas);
....
pxl.clear();
```

mask([radius])
--------------

Masks the selected area with pixelation.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
pxl.mask(10);
```

unmask()
--------

Unmasks the selected area, the area becomes transparent to reveal selected original.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
pxl.mask(10);
...
pxl.unmask();
```

pixelate()
----------

Pixelates the selected area and apply to the canvas.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
pxl.pixelate(10);
```

move(offsetX, offsetY)
----------------------

Moves the selected area to (offsetX, offsetY).

**Example usage**:

```js
var pxl = pixelate(canvas);
...
pxl.select(0, 0, 50, 50);
pxl.move(10, 20);
```

originalCanvas
--------------

Gets the original canvas specified when being initialized.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
var origin = pxl.originalCanvas;
```

currentCanvas
-------------

Gets the current canvas that could be pixelated or not.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
var origin = pxl.currentCanvas;
```

dispose()
---------

Unregisters this instance to specified canvas on initialize and dispose this instance.

This is useful to enable, disable pixelate functionality on the specified canvas.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
pxl.dispose();
```

getSelectedArea()
-----------------

Gets the selected area, this is immutable.

**Example usage**:

```js
var pxl = pixelate(canvas);
...
console.log(pxl.getSelectedArea());
```

Event triggers
==============

- `on('select:start', fn(x, y))`: when select start

- `on('select:stop', fn(x, y, selectedArea))`: when select stop

- `on('select:clear', fn(selectedArea))`: when clear selected area

- `on('mask', fn(radius, selectedArea))`: when mark selected area

- `on('unmask', fn(selectedArea))`: when unmark selected area

- `on('pixelate', fn(pixelatedCanvas))`: when pixelate the selected area

- `on('move', fn(offsetX, offsetY))`: when selected area move

- `on('dispose', fn())`: when dispose


[travis-url-master]: https://travis-ci.org/teracy-offcial/pixelate
[travis-image-master]: https://travis-ci.org/teracy-official/pixelate.svg?branch=master
[travis-url-develop]: https://travis-ci.org/teracy-offcial/pixelate
[travis-image-develop]: https://travis-ci.org/teracy-official/pixelate.svg?branch=develop
