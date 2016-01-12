# $

`$` is a query object providing a jQuery-like API for selecting and
manipulating the elements in the object tree.

## Selector

### $(_css-selector_)

```html
<cube/>
<cube id="foo" class="bar"/>
<cube class="bar"/>

<script>

  $('cube')
  // => all three cubes

  $('cube#foo')
  // => the cube whose id is 'foo'

  $('cube.bar')
  // => the two cubes with the 'bar' class label

</script>
```

## Properties

### .size()

Gets the size of the first matched element
```html
<cube t="size 10 20 30"/>
<script>
  $('cube').size()
  // => {x:10, y:20 z:30}
</script>
```

### .position()

Gets the position of the first matched element
```html
<cube t="position 10 20 30"/>
<script>
  $('cube').position()
  // => {x:10, y:20 z:30}
</script>
```

## Manipulating

### .t( _expression_ )

Perform the transform operations described in `expression` for each of
the matched elements.

```html
<sphere/>
<row spacing="10">
  <cube/>
  <cube/>
</row>

<script>
  // select the sphere and scale it up by 5
  $('sphere').t('scale 5')

  // select both cubes and translate them by (10,15,20)
  $('cube').t('translate 10 15 20')
</script>
```

### .l( _expression_ )

Perform the layout operations described in `expression`  on the matched elements.

```html
<cube/>
<cube id="middle"/>
<cube/>
<sphere/>
<script>
  // join all cubes along the x axis
  $('cube').l('join x')

  // select the middle cube and the sphere
  // place the sphere above the cube
  $('cube#middle').add('sphere')
    .l('join x')
</script>
```

## Traversing

### .get(i) or .get()

Retrieves the i-th matched elements. Or if no argument is given, Retrieves
all the matched elements.

### .add(selector)

Add elements to the set of currently matched elements.

```html
<cube/>
<sphere/>
<script>
  $('cube').add('sphere')
  // => [cube, sphere]

  $('sphere').add('cube')
  // => [cube, sphere]
</script>
```

### .find(selector)

Find selected descendants of each element in the current set of matched elements.
```html
<g class="foo">
  <cube id="one"/>
  <cylinder/>
</g>
<g class="foo">
  <cube id="two"/>
  <sphere/>
</g>
<script>
  $('.foo')
  // => [g, g]

  $('.foo').find('cube')
  // => [cube#one, cube#two]
</script>
```

### .children([selector])

Gets the children of the first selected element.
```html
<g class="foo">
  <cube id="one"/>
  <cylinder/>
</g>
<g class="foo">
  <cube id="two"/>
  <sphere/>
</g>
<script>
  $('.foo')
  // => [g, g]

  $('.foo').children()
  // => [cube#one, cylinder]
</script>
```

### .first()

Select the first element of the matched elements

```html
<cube id="one"/>
<cube id="two"/>  
<script>
  $('cube')
  // => [cube#one, cube#two] both cubes are selected

  $('cube').first().t('scale 2')
  // => only the cube#one is transformed

  $('cube').t('translate x 10')
  // => both cube#one and cube#two are translated by x = 10
</script>
```

### .last()

Select the last element of the matched elements

```html
<cube id="one"/>
<cube/>
<cube/>
<cube/>
<cube id="two"/>  
<script>
  $('cube')
  // => [cube#one, cube#two] both cubes are selected

  $('cube').last().t('scale 2')
  // => only the cube#two is scaled

  $('cube').t('translate x 10')
  // => all cubes are translated
</script>
```

### .filter(selector)

Iterates over, reducing the set of matched elements to those that match the selector.
```html
<row>
  <cube class="a"/>
  <cube class="a"/>
  <col>    
    <cube class="b"/>
    <cube class="b"/>
  </col>
</row>

<script>
  $('cube')
  // => [cube.a, cube.a, cube.b, cube.b]

  $('cube').filter('col .b')
  // => [cube.b, cube.b]

</script>
```
