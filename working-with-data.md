# Working with Data

## build items array with push like syntax

```twig
{% set items = [] %}

{% set items = items|merge([{
  width: 'two',
  content: include('@organisms/10-article-card-demo.twig'),
}]) %}

{% set items = items|merge([{
  width: 'one',
  content: include('@organisms/10-article-card-demo.twig'),
}]) %}

{% include '@base/_group-grid.twig' with {
  items: items,
} %}
```
