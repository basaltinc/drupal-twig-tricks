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

## A Good Strategy for starting files

```twig
{% set comp = node.field_competition.entity %}

{% set data = {
  location: node.field_location.value,
  has_audio: node.field_has_audio.value,
  comment: node.field_comment.value,
  score_opponent: node.field_score_opponent.value,
  highlights: node.field_match_highlights.value,
  competition: comp.field_name.value,
  competition_logo: comp.field_logo.entity.getFileUri() | image_style('small'),
} %}

{# Great for debugging; comment it when not needed #}
<ol>
  {% for key,value in data %}
    <li>{{ key }} - {{ value }}</li>
  {% endfor %}
</ol>
```

### Sidenote: how to crash Drupal with Twig

Since your twig templates can potentially access PHP Classes, if you access something you're not supposed to (like a private method or property), it can cause a white screen of death.

Assuming `data` has something that'll cause an error if accessed, take a peak at the difference between these two code snippets:

Due to `value` being accessed, it'll crash:

```twig
<ol>
  {% for key, value in data %}
    <li>{{ key }} - {{ value }}</li>
  {% endfor %}
</ol>
```

Due to `value` not being accessed, it won't crash, but you can see the key names:

```twig
<ol>
  {% for key,value in data %}
    <li>{{ key }}</li>
  {% endfor %}
</ol>
```
