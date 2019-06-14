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

## Full JSON output

```twig
<pre><code>{{ _context|json_encode(constant('JSON_PRETTY_PRINT')) }}</code></pre>
```

Be careful with a full `_context` output as that can be crazy in Drupal, often it's best to dump specific variables.
