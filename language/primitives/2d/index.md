# 2D Primitives

CraftML's built-in 2D primitives are:
* {{ 'circle' | tag}}
* {{ 'rectangle' | tag}}
* {{ 'triangle' | tag}}
* {{ 'polygon' | tag}}
* {{ 'path' | tag}}

{% craftml %}
<row spacing="5">
  <circle/>
  <rectangle/>
  <triangle/>
  <polygon points="0,0 10,0 10,10 5,15 0,10"/>
  <path d="M10 10 h 10 v 15 z"/>
</row>
{% endcraftml %}


## Useful Techniques

Even though 2D primitives will not be exported for 3D printing, they are useful
for a number of purposes.

### Spatial Markers

One useful technique is to use a 2D shape as a reference maker to perform
special layout that's hard to achieved using only the builtin layout operations,
such as {{ 'align' | attr}}, {{ 'flow' | attr}}, and {{ 'center' | attr}}.
2D shapes do participate in layout operations , but they do not get exported for 3D printing.

In the example below, we create a cylinder and place a couple circles to mark two distinct
areas on the front side of this cylinder. Next, we create a small blue cube and
a small green sphere. We use `$` in a script tag to select the circle whose id
is `marker1`, and then
add the cube to the selection to align this cube to that circle. Similarly, we
align the sphere with the other circle whose id is `marker2`.


{% craftml %}
<g>
  <cylinder height="20"
    style="opacity:0.9; color: yellow"/>

  <!-- define two circles as markers -->
  <circle t="rotate x 90; position 0 8 9"
    id="marker1"
    style="color: red"/>
  <circle t="rotate x 90; position 0 8 2"
    id="marker2"
    style="color: red"/>    
</g>

<cube t="scale 0.5" color="blue"/>
<sphere t="scale 0.5" color="green"/>

<script>
  // join the cube with #marker1
  $('circle#marker1').add('cube')
    .l('join y')

  // join the sphere with #marker2  
  $('circle#marker2').add('sphere')
    .l('join y')    
</script>
{% endcraftml %}
