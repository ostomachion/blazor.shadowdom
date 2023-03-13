# Blazor Shadow DOM
A modified version of Microsoft's Blazor JavaScript files to add support for shadow DOMs.

Development and testing happens in https://github.com/ostomachion/aspnetcore

Still in development, but mostly tested and functional for Blazor WebAssembly projects.

Also see [Blazor Web Components](https://github.com/ostomachion/blazor.webcomponents) for a library that turns Blazor components into real standards-based Web Components using custom elements, shadow DOM, and HTML templates.

## Installation

`dotnet add package Ostomachion.Blazor.V7_0_3.ShadowDom --version 1.0.0-preview2`

**Important:** Make sure that the package you download matches the version of ASP.NET Core that you are using. Currently only 7.0.3 is supported. **Other versions are coming soon!**

## Setup

### WebAssembly

In `wwwroot/index.html`, replace the Blazor script

```html
<script src="_framework/blazor.webassembly.js"></script>
```

with the Blazor Shadow DOM script

```html
<script src="_content/Ostomachion.Blazor.VX_X_X.ShadowDom/blazor.webassembly.js"></script>
```

replacing `VX_X_X` with the version Blazor you're using, e.g., `V7_0_3`.

### Server

In `Pages/_Host.html`, replace the Blazor script

```html
<script src="_framework/blazor.server.js"></script>
```

with the Blazor Shadow DOM script

```html
<script src="_content/Ostomachion.Blazor.VX_X_X.ShadowDom/blazor.server.js"></script>
```

replacing `VX_X_X` with the version Blazor you're using, e.g., `V7_0_3`.

### MAUI / WebView

In `wwwroot/index.html`, replace the Blazor script

```html
<script src="_framework/blazor.webview.js" autostart="false"></script>
```

with the Blazor Shadow DOM script

```html
<script src="_content/Ostomachion.Blazor.VX_X_X.ShadowDom/blazor.webview.js" autostart="false"></script>
```

replacing `VX_X_X` with the version Blazor you're using, e.g., `V7_0_3`.

## Usage

The new scripts modify the Blazor renderer to recognize [declarative shadow DOMs](https://developer.chrome.com/en/articles/declarative-shadow-dom/). In a `.razor` file, you can add a `template` element with a `shadowrootmode` attribute to get Blazor to attach a shadow root to the parent element.

```razor
<div id="host">
  <template shadowrootmode="open">
    <p>Shadow Content</p>
    <slot></slot>
  </template>
  <p>Light content</p>
</div>
```

This script was written to follow the declarative shadow DOM spec as closely as possible, so a normal template element will be rendered if the parent element cannot be a shadow host. Likewise, if the component does not define a parent for the template element, a normal template will be rendered no matter what the actual parent is at runtime.
