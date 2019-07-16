```
// _mixins.scss //
@import './shadows';
@import './icons';
@import './shapes';
@import './transforms';
```

_functions.scss
```
// return white or black to
// best contrast input color
@function contrast($color) {
    @if (lightness($color) > 40) {
      @return #000;
    }
    @else {
      @return #FFF;
    }
}
```

_transforms.scss
```
// generic transform ========================= //
@mixin transform($transforms) {
	   -moz-transform: $transforms;
	     -o-transform: $transforms;
	    -ms-transform: $transforms;
	-webkit-transform: $transforms;
          transform: $transforms;
}
// rotate ==================================== //
@mixin rotate($deg) {
  @include transform(rotate(#{$deg}deg));
}
 
// scale ===================================== //
@mixin scale($scale) {
	 @include transform(scale($scale));
} 

// translate ================================= //
@mixin translate($x, $y) {
   @include transform(translate($x, $y));
}

// skew ======================================= //
@mixin skew($x, $y) {
   @include transform(skew(#{$x}deg, #{$y}deg));
}

//transform origin ============================ //
@mixin transform-origin ($origin) {
    moz-transform-origin: $origin;
	     -o-transform-origin: $origin;
	    -ms-transform-origin: $origin;
	-webkit-transform-origin: $origin;
          transform-origin: $origin;
}
```
