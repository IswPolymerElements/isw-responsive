# \<isw-responsive\>

Provides feedback about device and orientation, using material design breakpoints.

https://material.io/guidelines/layout/responsive-ui.html#responsive-ui-breakpoints

Get device and orientation from the element ...
```
<isw-responsive device="{{device}}" orientation="{{orientation}}"></isw-responsive>
```

... and propagate it to elements implementing the behavior.
```
<isw-toolbar device="[[device]]" orientation="[[orientation]]">
    ...
</isw-toolbar>
```