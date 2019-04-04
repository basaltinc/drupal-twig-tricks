# Entities and Twig

## Helpful links

- [Entity reference values in twig template | Drupal.org](https://www.drupal.org/node/2636518)
- [Drupal 8 Entity Cheat Sheet | Drupal informatie van Wizzlern, de Drupal trainers](https://wizzlern.nl/drupal/drupal-8-entity-cheat-sheet)
- [Get referenced node fields in twig - Drupal Answers](http://drupal.stackexchange.com/questions/196876/get-referenced-node-fields-in-twig)

## Tips

If you want to access fields and their values, start off with node, not content, which is a render array with the configured fields.

---

when trying to figure out what's in a content entity, use node.toArray(), that gives you an array representation that's very close to how you can access it as an object. While the internal structure is quite different.

---

Then, you can access a field value with block\_content.field\_name.property. So in your case, block\_content.field\_align.value. The property is value for most field types, for references, you can either use target\_id for the ID or entity for the referenced entity object. Yes, you can directly access fields on that, but make sure to always check that a reference exists otherwise you can end up with fatal errors or exceptions. To access the label of a term reference for example, you can access it as block\_content.field\_tags.entity.name.value.

If you don't specify the field delta, it defaults to the first. If you want to access a different delta, you can use entity.field\_name.1.valueand so on. You can also loop over them.

This all maps directly to PHP, you can also do $block\_content-\>field\_tags-\>entity-\>name-\>value in preprocess and other places where you have the block\_content.

## Snippets

```twig
{{ node.field_blog_author.entity.title.value }}
```

