# Twig in PHP

Here is code that can be used in php files (like `theme_name.theme`) that help with working with Twig

## Get entire `TwigEnvironment`

```php
/** @var \Drupal\Core\Template\TwigEnvironment $twig */
$twig = \Drupal::service('twig');
```
