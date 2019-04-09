# Working with Drupal images

Assuming you have a `paragraph` of type `card`, with an image field of `field_my_image`. Then inside `paragraph--card.html.twig`:

```twig
{% set img = node.field_image.entity.getFileUri() %}
```

In `img`, you'll end ups with something like `public://images/ocean.jpg` that you still need to transform using an image style into an actual usable image path like `/files/image.jpg`.

Pass that through [Drupal's `file_url()` twig function](https://www.drupal.org/docs/8/theming/twig/functions-in-twig-templates#file_url) to get the actual root relative path:

```twig
{% set img = node.field_image.entity.getFileUri() %}
{# result: public://images/ocean.jpg #}

{% set imgUrl = file_url(img) %}
{# result: /sites/default/files/ocean.jpg #}

{# requires `twig_tweak` Drupal module #}
{% set smallImgUrl = img | image_style('small') %}
{# result: /sites/default/files/styles/medium/ocean.jpg #}
```

## Image Styles

If you've installed the `twig_tweak` Drupal module, then you can use this filter: `| image_style('small')`.

If you have the image styles `small` and `16x9` setup already, then you could do this:

```twig
image path is: {{ 'public://images/ocean.jpg' | image_style('thumbnail') }}
```

```twig
{% set img = paragraph.field_my_image.entity.getFileUri() %}
{# result: public://images/ocean.jpg #}

{% set imgUrl = file_url(img) %}
{# result: /sites/default/files/ocean.jpg #}

{% set smallImgUrl = img | image_style('small') %}
{# result: /sites/default/files/styles/small/ocean.jpg #}

{% panoImgUrl = img | image_style('16x9') %}
{# result: /sites/default/files/styles/16x9/ocean.jpg #}
```

### Nested Entity References

```twig
{% set img = node.field_featured_image.entity.field_image.entity.getFileUri() %}

{% set badWayToGetImg = content.field_player.0['#node'].field_listing_image.entity.field_image.0.entity.getFileUri() }
```
