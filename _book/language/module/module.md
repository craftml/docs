# module

[craftml.io](https://craftml.io/) is an online platform for the community to
easily create, edit, and share their CraftML models. Each model file on
[craftml.io](https://craftml.io/) is a reusable module and has a unique identifier
for importing. For example, the model file at [http://craftml.io/4yS59](http://craftml.io/4yS59)
is a heart, created by [calebhsu](http://craftml.io/~calebhsu). The module id
is `4yS59`. Knowing this, we can import this model and pick a meaningful tag
name, for instance, _heart_, like the code below.

```html
<!-- create a heart using the module @ 4yS59 -->
<heart module="4yS59"/>
```

{% craftml %}
<!-- create a heart using the module @ 4yS59 -->
<heart module="4yS59"/>
{% endcraftml %}
