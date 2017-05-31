# Dynamic Slick slider
[![N|Solid](http://kenwheeler.github.io/slick/img/slick.gif)](http://kenwheeler.github.io/slick/)

## Разширение Slick slider для аккуратного отображения множества элементов на меньших устройствах

### Demo 
[codepen.io/JoyZi/](https://codepen.io/JoyZi/pen/LygBgr)

### Extension settings

Option | Type | Default 
------ | ---- | ------- 
maxWidth | number | 1024 
getWidth | function | $( window ).width 


```javascript
// slickDynamic extension for Slick carousel by vereschak@gmail.com
( function ( $ ) {
    $.fn.slickDynamic = function ( options, breakpoints ) {
        var bs = $.extend( {
            "maxWidth": 1024,
            "getWidth": $( window ).width
        }, breakpoints );
        var slider = this;
        slider.attr( 'data-dynamic', 'offslider' );
        slider.resize = function () {
            slider.each( function ( index, el ) {
                var self = $( this );
                if ( bs.getWidth() < bs.maxWidth && !self.hasClass( 'slick-slider' ) ) {
                    self.slick( options );
                    self.attr( 'data-dynamic', 'onslider' );
                } else if ( bs.getWidth() >= bs.maxWidth && self.hasClass( 'slick-slider' ) ) {
                    self.slick( 'unslick' );
                    self.attr( 'data-dynamic', 'offslider' );
                }
            } );
        };
        ( function ( slider ) {
            $( window ).on( "resize", slider.resize.bind( slider ) );
        } )( slider );
        slider.resize();
        return slider;
    };
} )( jQuery );

$( document ).ready( function () {
    // $( slider ).slickDynamic( { slick settings }, { extension settings } );
    $( ".current_items" ).slickDynamic( {
        slidesToShow: 1,
        slidesToScroll: 1,
        arrows: false,
        dots: false
    }, {
        getWidth: viewport.width
    } );
} );

```

