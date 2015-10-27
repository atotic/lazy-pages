# lazy-pages
##### when you do not want all your pages to get out of bed at once

Status: beta

Instead of your app
```html
<neon-animated-pages selected="{{selected}}">
  <landing-page></landing-page>
  <demo-page></demo-page>
  <contact-page></contact-page>
</neon-animated-pages>
```
loading every page into DOM on startup, use `lazy-pages` to load them on demand:
```html
<lazy-pages>
  <!-- very-important-page is not loaded lazily -->
  <very-important-page></very-important-page>

  <template is="dom-if">
    <!-- landing-page is displayed lazily, stays in dom once shown -->
    <landing-page></landing-page>
  </template>

  <template is="dom-if" restamp>
    <!-- demo-page is displayed lazily, and removed from dom when invisible -->
    <demo-page></demo-page>
  </template>

</lazy-pages>

```

### Why?
- memory: you have lots of pages, and do not want to load them all at once on startup
- speed: you do not want to load all your element definitions on startup
- attached callbacks: you do not want all your attached callbacks to run on an initial load

### Usage

`lazy-pages` will render just like `neon-animated-pages`. You can also use them as `iron-pages` replacement.

Put any template you'd like to load lazily inside a `dom-if` template:

```html
<template is="dom-if">
  <my-page></my-page>
</template>
```

You can only have a single top-level tag inside a template (except for link tags). This keeps my code simple.

To remove element from dom when invisible, use `restamp` dom-if option.

`lazy-pages` has basic attribute compatibility with neon-animated-pages: `selected`, `attrForSelected`, `animateInitialSelection`, `items`, `selectedItem`.

### Not working

It'd be nice to also load element definitions lazily. My initial hack was
to allow &lt;link&gt; elements inside dom-if templates. It worked everywhere but IE.
I think it can be made to work, but I am not sure if this is the right way to do it.
Another idea was to have a map of {unresolved-tag-name -> import link}, traverse templates
for any unresolved elements, and importHref definitions when elements are shown.

This is how it used to work:
```html
 <!-- this example does not work in IE still working on a workaround -->
  <template is="dom-if">
    <!-- super-complex-page element definition is also loaded lazily -->
    <link rel="import" href="super-complex-page.html">
    <super-complex-page></super-complex-page>
  </template>
```

