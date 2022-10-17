---
layout: docs
title: Color modes
description: Bootstrap now supports color modes, or themes, as of v5.3.0. Explore our default light theme and new dark mode theme, or create your own using our themes as your template.
group: customize
toc: true
prev: color
next: components
---

{{< added-in "5.3.0" >}}

## Dark mode

**Bootstrap now supports color modes, starting with dark mode!** With v5.3.0 you can implement your own color mode toggler (see below for an example from Bootstrap's docs) and apply the different color modes as you see fit. We support a light mode (default) and now dark mode. Color modes can be toggled globally on the `<html>` element, or on specific components and elements, thanks to the `data-bs-theme` attribute.

Alternatively, you can also switch to a media query implementation thanks to our color mode mixin—see [the usage section for details](#usage). Heads up though—this eliminates your ability to change themes on a per-component basis as shown below.

### Example

For example, to change the color mode of a dropdown menu, add `data-bs-theme="light"` or `data-bs-theme="dark"` to the parent `.dropdown`. Now, no matter the global color mode, these dropdowns will display with the specified theme value.

{{< example class="d-flex justify-content-between" >}}
<div class="dropdown" data-bs-theme="light">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonLight" data-bs-toggle="dropdown" aria-expanded="false">
    Default dropdown
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonLight">
    <li><a class="dropdown-item active" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
    <li><a class="dropdown-item" href="#">Something else here</a></li>
    <li><hr class="dropdown-divider"></li>
    <li><a class="dropdown-item" href="#">Separated link</a></li>
  </ul>
</div>

<div class="dropdown" data-bs-theme="dark">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonDark" data-bs-toggle="dropdown" aria-expanded="false">
    Dark dropdown
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonDark">
    <li><a class="dropdown-item active" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Action</a></li>
    <li><a class="dropdown-item" href="#">Another action</a></li>
    <li><a class="dropdown-item" href="#">Something else here</a></li>
    <li><hr class="dropdown-divider"></li>
    <li><a class="dropdown-item" href="#">Separated link</a></li>
  </ul>
</div>
{{< /example >}}

### How it works

We've implemented...

## Nesting color modes

Use `data-bs-theme` on a nested element to change the color mode for a group of elements or components. In the example below, we have an outer dark mode with a nested light mode. You'll notice components naturally adapt their appearance without modification, but the nested `data-bs-theme="light"` needs help to reset some global styles. This is because `data-bs-theme` doesn't reset the globally declared `<body>` colors, so we have to add `.bg-body` and `.text-body`.

{{< example class="" >}}
<div data-bs-theme="dark">
  <nav aria-label="breadcrumb">
    <ol class="breadcrumb">
      <li class="breadcrumb-item"><a href="#">Color modes</a></li>
      <li class="breadcrumb-item active" aria-current="page">Dark</li>
    </ol>
  </nav>

  <p>This should be shown in a <strong>dark</strong> theme at all times.</p>

  <div class="progress mb-4">
    <div class="progress-bar" role="progressbar" aria-label="Basic example" style="width: 25%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div>
  </div>

  <div class="dropdown mb-4">
    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonDark2" data-bs-toggle="dropdown" aria-expanded="false">
      Dark dropdown
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonDark2">
      <li><a class="dropdown-item active" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Another action</a></li>
      <li><a class="dropdown-item" href="#">Something else here</a></li>
      <li><hr class="dropdown-divider"></li>
      <li><a class="dropdown-item" href="#">Separated link</a></li>
    </ul>
  </div>

  <div data-bs-theme="light" class="p-3 bg-body text-body rounded">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="#">Color modes</a></li>
        <li class="breadcrumb-item"><a href="#">Dark</a></li>
        <li class="breadcrumb-item active" aria-current="page">Light</li>
      </ol>
    </nav>

    <p>This should be shown in a <strong>light</strong> theme at all times.</p>

    <div class="progress mb-4">
      <div class="progress-bar" role="progressbar" aria-label="Basic example" style="width: 25%" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div>
    </div>

    <div class="dropdown">
      <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonLight2" data-bs-toggle="dropdown" aria-expanded="false">
        Light dropdown
      </button>
      <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonLight2">
        <li><a class="dropdown-item active" href="#">Action</a></li>
        <li><a class="dropdown-item" href="#">Action</a></li>
        <li><a class="dropdown-item" href="#">Another action</a></li>
        <li><a class="dropdown-item" href="#">Something else here</a></li>
        <li><hr class="dropdown-divider"></li>
        <li><a class="dropdown-item" href="#">Separated link</a></li>
      </ul>
    </div>
  </div>
</div>
{{< /example >}}

## Usage

Our new dark mode option is enabled by default for all users of Bootstrap. You can disable our dark mode via Sass by changing `@enable-dark-mode` to `false`.

In addition, we use a custom Sass mixin, `color-mode()`, to help you control _how_ color modes are applied. By default, we use a `data` attribute approach, allowing you to create more user-friendly experiences where your visitors can choose to have an automatic dark mode or control their preference (like in our own docs here). This is also an easy way to add different themes and more custom color modes beyond light and dark.

In case you want to use media queries and only make color modes automatic, you can change the mixin's default type via Sass variable. Consider the following snippet and it's compiled CSS output.

```scss
@color-mode-type: data !default;

@include color-mode(dark) {
  .element {
    color: var(--bs-primary-text);
    background-color: var(--bs-primary-bg-subtle);
  }
}
```

Outputs to:

```css
[data-bs-theme=dark] .element {
  color: var(--bs-primary-text);
  background-color: var(--bs-primary-bg-subtle);
}
```

And when setting to `media-query`:

```scss
@color-mode-type: media-query;

@include color-mode(dark) {
  .element {
    color: var(--bs-primary-text);
    background-color: var(--bs-primary-bg-subtle);
  }
}
```

Outputs to:

```css
@media (prefers-color-scheme: dark) {
  .element {
    color: var(--bs-primary-text);
    background-color: var(--bs-primary-bg-subtle);
  }
}
```

## Custom color modes

While the primary use case for color modes is light and dark mode, custom color modes are also possible. Create your own `data-bs-theme` selector with a custom value as the name of your color mode, then modify our Sass and CSS variables as needed. We opted to create a separate `_variables-dark.scss` stylesheet to house Bootstrap's dark mode specific Sass variables, but that's not required for you.

For example, you can create a "blue theme" with the selector `data-bs-theme="blue"`. In your custom Sass or CSS file, add the new selector and override any global or component CSS variables as needed. If you're using Sass, you can also use Sass's functions within your CSS variable overrides.

{{< scss-docs name="custom-color-mode" file="site/assets/scss/_content.scss" >}}

<div class="bd-example text-body bg-body" data-bs-theme="blue">
  <div class="h4">Example blue theme</div>
  <p>Some paragraph text to show how the blue theme might look with written copy.</p>

  <hr class="my-4">

  <div class="dropdown">
    <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonCustom" data-bs-toggle="dropdown" aria-expanded="false">
      Dropdown button
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonCustom">
      <li><a class="dropdown-item active" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Action</a></li>
      <li><a class="dropdown-item" href="#">Another action</a></li>
      <li><a class="dropdown-item" href="#">Something else here</a></li>
      <li><hr class="dropdown-divider"></li>
      <li><a class="dropdown-item" href="#">Separated link</a></li>
    </ul>
  </div>
</div>

```html
<div data-bs-theme="blue">
  ...
</div>
```
