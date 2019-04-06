# Working with Drupal images

Assuming you have a `paragraph` of type `card`, with an image field of `field_my_image`. Then inside `paragraph--card.html.twig`:

```twig
{% set img = node.field_image.entity.getFileUri() %}
```

In `img`, you'll end ups with something like `public://images/ocean.jpg` that you still need to transform using an image style into an actual usable image path like `/files/image.jpg`.

## Image Styles

If you've installed the `twig_tweak` Drupal module, then you can use this filter: `| image_style('small')`.

If you have the image styles `small` and `16x9` setup already, then you could do this:

```twig
image path is: {{ 'public://images/ocean.jpg' | image_style('thumbnail') }}
```

```twig
{% set img = node.field_featured_image.entity.field_image.entity.getFileUri() %}

{% smallImg = img | image_style('small') %}
{% panoImg = img | image_style('16x9') %}
```

### Nested Entity References

```twig
{% set img = node.field_featured_image.entity.field_image.entity.getFileUri() %}

{% set badWayToGetImg = content.field_player.0['#node'].field_listing_image.entity.field_image.0.entity.getFileUri() }
```
