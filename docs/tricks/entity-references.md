# Entity References

```twig
{% set venueCity = paragraph.field_venue.entity.field_city.value %}
```

It can be helpful to set the `entity` to a variable so accessing it's fields feels more straightforward:

```twig
{% set venue = paragraph.field_venue.entity %}

{% set venueCity = venue.field_city.value %}
{% set venueState = venue.field_state.value %}
```
