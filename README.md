This repository contains a collection of generic SCSS mixins and functions I use on almost all of my web projects. A handful of them follow a lookup table pattern.

## Look up tables

The lookup table pattern consists of a set of files in `scss/settings/` and `scss/tools/`. The idea behind this method is the configuration is defined in `settings` and the function to access these configuration values is located in `tools`. The settings configuration should never be accessed directly in your code. All access to settings occurs through the lookup function. The main problem this pattern solves is scoping your variables. Instead of `$red` or `$breakpointMobile` you have `color(red)` and `breakpoint(mobile)`.

An example can be seen with `colors.scss`.

`settings/colors.scss`

```scss
$colors: (
  black: #000000,
  white: #FFFFFF,
);
```

`tools/colors.scss`

```scss
@function color($name) {
  $color: map-get($colors, $name);
  @if($color) {
    @return $color;
  }
  @else {
    @warn "#{$name} is not a valid color";
    @return null;
  }
}
```

`components/example.scss`

```scss
.example {
  color: color(white);
}
```