# this

`this` refers to the solid element that contains the script block.

```html
<g id="foo">
	<cube></cube>
	<script>
		this.id
		// => foo

		this.children
		// => [cube]
	</script>
</g>
```

`this.children` only contains solid elements constructed right _before_ the script block; it does not contain solid elements _after_ the script block that have not yet been constructed.

```html
<g id="foo">
	<cube></cube>
	<script>
		this.id
		// => foo

		this.children
		// => [cube]
	</script>
	<sphere></sphere>
</g>
```

In addition, source elements that do not generate solids will not be parts of  `this.children`.

```html
<g id="foo">
	<param name="foo" type="int"/>
	<craft name="bar" module="XYZ123"/>
	<cube></cube>
	<script>
		this.id
		// => foo

		this.children
		// => [cube]
	</script>
	<sphere></sphere>
</g>
```


## Adding Elements

```html
// source DOM
<g>
	<cube></cube>
	<script>
		this.add('<sphere></sphere>')
	</script>
</g>

// => solid DOM
<g>
	<cube></cube>
	<sphere></sphere>
</g>
```

The transformation between a source element and a solid element is not necessarily an one-to-one relationship. A source element may generate one or more solid elements or even none at all.

```html
// source DOM
<param name="a" type="int"/>
<craft name="bar" module="craft-bar"/>
<cube></cube>

// => solid DOM
<cube></cube>
```

Similarly, a script tag can add more than one solid elements to the solid DOM.

```html
// source DOM
<g>
	<sphere></sphere>
	<script>
		this.add('<cube></cube>')
		this.add('<cube></cube>')
	</script>
</g>

// => solid DOM
<g>
	<sphere></sphere>
	<cube></cube>
	<cube></cube>
</g>
```

Or it can add none at all.

```html
// source DOM
<g>
	<sphere></sphere>
	<script>
		// does nothing
	</script>
</g>

// => solid DOM
<g>
	<sphere></sphere>
</g>
```

Here are more examples.

```javascript
// add a cube
this.add('<cube></cube>')

// add a sphere
this.add('<sphere></sphere>')

// add a cube with parameters
this.add('<cube size="10 5 5"></cube>')

// add a cube with template parameters
this.add('<cube size="{{s}} 5 5"></cube>')

// add multiple cubes
this.add('<cube/><cube/><cube/><cube/>')
```

### Asynchronous Construction

Solid elements are constructed _asynchronously_. Why? Concurrency. Some elements may wait for files to be downloaded over the network. While waiting, the rendering engine can start working on constructing other elements, rather than being stuck waiting.

Consider the example below. Suppose the construction of `<remote-object>` involves downloading an STL file, which takes 1 second. The call to `this.add` will return immediately instead of blocking for 1 second. If we try to access the size of `<remote-object>` in the next line, we will get `undefined` because the object is still being constructed.

```html
<g>
	<cube></cube>
	<script>
		this.add('<remote-object></remote-object>')
		// return immediately

		this.children[1].size
		// => undefined
	</script>
</g>
```

What if we need to access the size or location of `<remote-object>`? We can do that in the next script block like this.

```html
<g>
	<cube></cube>
	<script>
		this.add('<remote-object></remote-object>')
		// return immediately
	</script>
	<script>
		this.children[1].size
		// => {x: 10, y:10, z:10}
	</script>
</g>
```

The rendering engine ensures that all the pending child elements will get fully constructed before executing a new script block. In other words, solid elements added in one script block may not necessarily be fully constructed within the same script block, but will certainly be fully constructed before the next script block begins.

Q: Are transformation and layout methods also asynchronous?

No. All transformation and layout methods are synchronous because they are compute-bound operations (matrix mulplitcations ... etc.) and do not involve I/O operations.

```html
<g>
	<cube></cube>
	<script>
		var c = this.children[0]
		// => c === <cube>

		c.size.x
		// => 10

		c.scale(2)

		c.size.x
		// => 20 (the effect is immediate)
	</script>
</g>
```
