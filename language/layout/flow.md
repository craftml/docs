# flow

{{ 'flow' | l}} puts each child right after the previous child along selected
dimensions so that they appear to _flow_ along these dimensions,
while keeping the first child at its
original position. A number can be optionally provided to indicate how much
space to leave between every two objects.

Let's consider a simple case involving two objects, a cube and a sphere. Initially,
they are overlapping; we can only see a cube because of this. After
adding `l="flow=x"` to `<g>`, the sphere is moved such that it is next to the cube,
no longer overlapping with it.

{% craftml %}
<!-- originally, they are all overlapping -->
<g>
  <cube/>
  <sphere/>
</g>

<!-- now they are adjacent -->
<g l="flow x" t="position y 20">
  <cube/>
  <sphere/>
</g>

<!-- spacing = 2 -->
<g l="flow x 2" t="position y 40">
  <cube/>
  <sphere/>
</g>

{% endcraftml %}

Let's look at an example with more objects involved. This time,
we have a cube and three spheres forming a group.
Initially, they are all overlapping. By adding `l="flow x"` to `<g>`,
they are rearranged into a line along the _x_ axis where each child is next to
the previous child.

{% craftml %}
<!-- originally, they are all overlapping -->
<g>
  <cube/>
  <sphere/>
  <sphere/>
  <sphere/>
</g>

<!-- flow in the x direction -->
<g l="flow x" t="position y 20">
  <cube/>
  <sphere/>
  <sphere/>
  <sphere/>
</g>

<!-- a spacing of 5 is added -->
<g l="flow x 5" t="position y 40">
  <cube/>
  <sphere/>
  <sphere/>
  <sphere/>
</g>
{% endcraftml %}

It is possible to flow in multiple directions simultaneously.
{% craftml %}
<g l="flow xy 2">
  <cube/>
  <sphere repeat="5"/>
  <sphere/>
  <sphere/>
</g>
{% endcraftml %}
