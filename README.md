# \<isw-responsive\>

`isw-responsive` calculates `device` and `orientation` according to material design breakpoints
and pushes the result to all elementes using `isw-responsive-behavior` using `iron-meta` and `iron-signals` like events.

If there will be an `iron-signals` 2.0, the element will be updated to use it instead of custom `document` events.

https://material.io/guidelines/layout/responsive-ui.html#responsive-ui-breakpoints

## `isw-responsive`

Calculates `device` and `orientation` from the current screen size.

Use it only once in your app, it will notify all `isw-responsive-behavior` elements about changes.

### `isw-responsive`

Provides `reflectToAttribute` properties for css selectors, and events for imperative use.

## `iron-meta`

`isw-responsive` writes the viewport information to `iron-meta`, so they are global available via these keys:

* isw-responsive-device
* isw-responsive-orientation

## `iron-signals`

Future plans: If `iron-signals` will get an 2.0 update, the `viewport-changed` event should be exposed to `iron-signals`., e.g.:

* isw-responsive-viewport-changed

## Example: Useage with Starter Kit.

my-app.html
```html
[...]

<!-- ISW Responsive imports -->
<link rel="import" href="../bower_components/isw-responsive/isw-responsive.html">
<link rel="import" href="../bower_components/isw-responsive/isw-responsive-behavior.html">

[...]

<dom-module id="my-app">
  <template>
    [...]

    <!-- isw-responsive definition that does the calculating and notifying. -->
    <isw-responsive></isw-responsive>

    [...]

    <!-- Deactivate app drawers responsive behavior for imperative example. -->
    <app-drawer-layout fullbleed responsive-width="0" force-narrow="[[_forceNarrow]]">

      [...]

    </app-drawer-layout>
  </template>

  <script>
    // Use Polymer.mixinBehaviors to assign the behavior to get device and orientation properties that reflect to attribute.
    class MyApp extends Polymer.mixinBehaviors([ iswResponsiveBehavior ], Polymer.Element ) {
      static get is() { return 'my-app'; }

      [...]

      constructor() {
        super();
        this.addEventListener( 'viewport-changed', e => this._viewportChanged( e ) );
      }

      [...]

      _viewportChanged() {
        // Manually set the drawers force narrow property depending on device and orientation (Imperative use example).
        switch( this.device ) {
          case 'desktop':
            this.set( '_forceNarrow', false );
            break;
          case 'tablet':
            this.set( '_forceNarrow', this.orientation == 'portrait' );
            break;
          default:
            this.set( '_forceNarrow', true );
        }
      }
    }
    window.customElements.define(MyApp.is, MyApp);
  </script>
</dom-module>
```

my-view1.html
```html
[...]
<!-- ISW Responsive imports -->
<link rel="import" href="../bower_components/isw-responsive/isw-responsive-behavior.html">
[...]

<dom-module id="my-view1">
  <template>
    <style include="shared-styles">
      :host {
        display: block;
        padding: 10px;
      }

      // Use attribute selectors to assign css properties for certain devices or / and orientations.
      :host([device="desktop"]) .card {
        ...
      }
      :host([device="mobile"][orientation="landscape"]) .card {
        ...
      }
    </style>

    <div class="card">
      [...]
    </div>
  </template>

  <script>
    // Use Polymer.mixinBehaviors to assign the behavior to get device and orientation properties that reflect to attribute.
    class MyView1 extends Polymer.mixinBehaviors([ iswResponsiveBehavior ], Polymer.Element ) {
      static get is() { return 'my-view1'; }
    }
    window.customElements.define(MyView1.is, MyView1);
  </script>
</dom-module>
```
