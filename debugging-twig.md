# Debugging Twig

## Poor man's debug

This will print all the keys of all data available. We don't print `value` as that can sometimes throw a fatal error in Drupal b/c it's trying to access a private property or class.

```twig
<ol>
  {% for key,value in _context %}
    <li>{{ key }}</li>
  {% endfor %}
</ol>
```
