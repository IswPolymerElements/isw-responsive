# \<isw-responsive\>

Provides feedback about device and orientation, using material design breakpoints.

https://material.io/guidelines/layout/responsive-ui.html#responsive-ui-breakpoints

Consists of an behavior and an element.
Behavior: Provides reflectToAttribute properties for propagation and css selectors.
Element: Checking and evaluating screen size and provides device and orientation values.

Example: Useage with Starter Kit.

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

    <!-- Definition, bindings, event listener for changes. -->
    <isw-responsive
        device="{{device}}"
        orientation="{{orientation}}"
        on-screen-changed="_screenChanged">
    </isw-responsive>

    [...]

    <!-- Deactivate app drawers responsive behavior for imperative example. -->
    <app-drawer-layout fullbleed responsive-width="0" force-narrow="[[_forceNarrow]]">
      <!-- Drawer content -->
      [...]

      <!-- Main content -->
      <app-header-layout has-scrolling-region>

        [...]

        <iron-pages
            selected="[[page]]"
            attr-for-selected="name"
            fallback-selection="view404"
            role="main">
          <!-- Propagate device and orientation to the views. -->
          <my-view1 name="view1" device="[[device]]" orientation="[[orientation]]"></my-view1>
          <my-view2 name="view2" device="[[device]]" orientation="[[orientation]]"></my-view2>
          <my-view3 name="view3" device="[[device]]" orientation="[[orientation]]"></my-view3>
          <my-view404 name="view404"></my-view404>
        </iron-pages>
      </app-header-layout>
    </app-drawer-layout>
  </template>

  <script>
    // Use Polymer.mixinBehaviors to assign the behavior to get device and orientation properties that reflect to attribute.
    class MyApp extends Polymer.mixinBehaviors([ iswResponsiveBehavior ], Polymer.Element ) {
      static get is() { return 'my-app'; }
      [...]

      _screenChanged() {
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
