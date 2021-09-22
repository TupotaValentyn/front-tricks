###Tag  `<head>`

---
#### About `<head>` : 

* #### Category: None.
* #### Context in witch this element can be used: As the first element in an `html` element.
* #### Content model: If the document is an [`iframe srcdock document`](https://html.spec.whatwg.org/#an-iframe-srcdoc-document) or if the title information is available from higher-level protocol. Zero or more elements of [metadata content](https://html.spec.whatwg.org/#metadata-content-2), of which no more than one is a [`title`](https://html.spec.whatwg.org/#the-title-element) element and no more than one is a [`base`](https://html.spec.whatwg.org/#the-base-element) element.
  Otherwise: One or more elements of [metadata content](https://html.spec.whatwg.org/#metadata-content-2), of which no more than one is a [`title`](https://html.spec.whatwg.org/#the-title-element) element and no more than one is a [`base`](https://html.spec.whatwg.org/#the-base-element) element.
* #### Tag omission in text/html: 
  * A [`head`](https://html.spec.whatwg.org/#the-head-element) element's [start tag](https://html.spec.whatwg.org/#syntax-start-tag) can be omitted is the element is empty, or if the first thing inside the `head` element is an element;
  * A [`head`](https://html.spec.whatwg.org/#the-head-element) element's [end tag](https://html.spec.whatwg.org/#syntax-end-tag) can be omitted is the `head` element is not immediately followed by [ASCII whitespace](https://infra.spec.whatwg.org/#ascii-whitespace) or a [comment](https://html.spec.whatwg.org/#syntax-comments).
* #### Content attributes: [Global attributes](https://html.spec.whatwg.org/#global-attributes)
* #### Accessibility considerations:
  * [For authors](https://w3c.github.io/html-aria/#el-head);
  * [For implementers](https://w3c.github.io/html-aam/#el-head);
* #### DOM interface:
```ts
[Exposed = Window]
  interface HTMLHeadElement: HTMLElement {
    [HTMLConstructor]: constructor();
}
```
---
#### The `head` element [represents](https://html.spec.whatwg.org/#represents) a collection of metadata for the [`Document`](https://html.spec.whatwg.org/#document).
`[Elements in the DOM represent things; that is, they have intrinsic meaning, also known as semantics.]`

---

## `Example`

The collection of metadata in a `head` element can be large or small. Here is an example of a very short one:

```html
<!doctype html>
<html lang=en>
 <head>
  <title>A document with a short head</title>
 </head>
 <body>
 ...
```

Here is an example of a long one: 

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <base href="https://www.example.com/">
  <title>an application with a long head</title>
  <link rel="stylesheet" href="default.css">
  <link rel="stylesheet alternate" href="big.css" title="big text">
  <script src="support.js"></script>
  <meta name="application-name" content="long headed application">
</head>
<body>
...
```

## `Note`
    The title element is a required child in most situations, but when a higher-level protocol provides title information, e.g. in the Subject line of an email when HTML is used as an email authoring format, the title element can be omitted.
---

### Table of contents (for authors):

| Name  | Value |
|---|---|
| [[wai-aria-1.1]](https://w3c.github.io/html-aam/#bib-wai-aria-1.1)  |  No corresponding role |
| [MSAA + IAccessible2](http://accessibility.linuxfoundation.org/a11yspecs/ia2/docs/html/)  | Not mapped  |
| [UIA](https://docs.microsoft.com/en-us/previous-versions//ms726297(v=vs.85)?redirectedfrom=MSDN) | Not mapped |
| [ATK](https://gnome.pages.gitlab.gnome.org/atk/) | Not mapped|
| [AX](https://developer.apple.com/documentation/appkit/nsaccessibility) | Not mapped |

### Table of contents (for implementors):

| HTML element  | Implicit ARIA semantics (explicitly assigning these in markup is NOT RECOMMENDED) | ARIA roles, states and properties which MAY be used |
|---|---|---|
| `head`  | [No corresponding role](https://w3c.github.io/html-aria/#dfn-no-corresponding-role)  |  No `role` or `aria-*` attributes |

#### Default structure:

```html
<!doctype html>
<html lang="en">
<head></head>

<style>

  html, body {
    height: 100%;
    margin: 0;
    padding: 0;
  }

  html {
    display: grid;
    place-content: center;
  }

</style>
</html>
```

#### Tag `<head>` can't have content;

if you try to include content inside `head` tag, like this:

```html
<!doctype html>
<html lang="en">
<head>228</head>

...
```

in browser you will see the next structure:

```html
<!doctype html>
<html lang="en">
<head></head>
<body>
  228
</body>
...
```

By default browser cut all content from `head` and include this content in `body`; except [`title`, `meta`, `script`, `style`, and info tags];

Also if you try to add some `html` tags for content, you will see the same behavior;
For example: 
```html
<!doctype html>
<html lang="en">
<head>
  <div><228</div>
</head>
...
```

In browser:

```html
<!doctype html>
<html lang="en">
<head></head>
<body>
  <div><228</div>
...
```

---

If you have something like this: 

```html
<!doctype html>
<html lang="en">
<head></head>

<style>

  html, body {
    height: 100%;
    margin: 0;
    padding: 0;
  }

  html {
    display: grid;
    place-content: center;
  }

</style>
</html>
```

Tag `style` will be inside the tag `head`; 
But if you will add any content inside tag head except `meta-tags`:

```html
<!doctype html>
<html lang="en">
<head>228</head>
<style>
  ...
```

you will see the next structure:

```html
<!doctype html>
<html lang="en">
<head></head>
<body>
  228
  <style>
    html, body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
    
    html {
      display: grid;
      place-content: center;
    }
  </style>
</body>
</html>
```

---

### Interesting cases 

If you try to combine tags inside `head` and outside like this: 

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="Big5">
</head>
<style>
  ...
```

In browser you will see:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="Big5">
  <style>
    ...
  </style>
</head>

```

The browser concatenates the tags and inserts all tags inside the `head`;
