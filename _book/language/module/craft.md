# craft

{% craftml %}
<craft name="three-by-three-cubes">
  <col spacing="2">
    <repeat n="3">
      <row spacing="2">
        <repeat n="3">
            <cube></cube>
        </repeat>
      </row>
    </repeat>
  </col>
</craft>

<three-by-three-cubes></three-by-three-cubes>
{% endcraftml %}


## Importing from craftml.io

[craftml.io](https://craftml.io/) is an online platform for the community to
easily create, edit, and share their CraftML models. Each model on
[craftml.io](https://craftml.io/) has a unique identifier you can use to import
into your own model.

For example, craft [4yS59](http://craftml.io/4yS59) is a heart, created by [calebhsu](http://craftml.io/~calebhsu).
You can import this model and give it any name, say _heart_.

{% craftml %}
<heart module="4yS59"/>
{% endcraftml %}
