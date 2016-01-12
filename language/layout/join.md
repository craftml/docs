# join

{{ 'join' | l}} joins all children into an array-like structure along
a given dimension. The first child remains fixed in its original position.
the rest of the children are arranged to form a line on the _min_ or
_max_ side of this first child, and they are centered along the other
two dimensions

Let's consider a simple case involving a large cube and a bunch of small cubes. Initially,
they are overlapping; we can only see the large cube because of this. After
adding `l="join x"` to `<g>`, all small cubes are moved to join the large cube
to form a line along the _x_ axis; and all are centered with respect
to the large cube.

{% craftml %}
<!-- initially, all cubes are overlapping -->
<g l=""
   t="position x 0">
  <cube t="scale 2"
        style="color:red; opacity: 0.6"/>
  <cube/>
  <cube/>
  <cube/>
  <cube/>
</g>

<!-- now, cubes are joined into a line -->
<g l="join y"
   t="position x 25">
  <cube t="scale 2" color="red"/>
  <cube/>
  <cube/>
  <cube/>
</g>
{% endcraftml %}

{{ 'join' | l}} can optionally take a number, such as `join x 3` to specify how much space
to put between every two objects.

{% craftml %}
<!-- spacing = -2 -->
<g l="join y -2"
   t="position x 0">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="yellow"/>
</g>

<!-- spacing = 0-->
<g l="join y"
   t="position x 25">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="yellow"/>
</g>

<!-- spacing = 5 -->
<g l="join y 5"
   t="position x 50">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="yellow"/>
</g>
{% endcraftml %}

A side _min_ or _max_ can be specified to indicate which side of the first child
to join the rest of the children to.

{% craftml %}
<g l="join x min">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="green"/>
</g>

<g l="join y min"
   t="position x 25">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="blue"/>
</g>

<g l="join y max"
   t="position x 50">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="skyblue"/>
</g>

<g l="join z max"
   t="position x 75">
  <cube t="scale 2" color="red"/>
  <cylinder repeat="3" color="purple"/>
</g>
{% endcraftml %}
