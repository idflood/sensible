# sensible

With `Sensible` you can maintain your media-queries where they belong; in your SASS/SCSS and make them available with the same name space in your JS without polluting your HTML. 

Demo: http://codepen.io/meodai/pen/kzwAy?editors=011

## Setup
`bower install sensible --save-dev`

import **_mediaqueries.scss** to you main scss/sass file.
	
	@import 'mediaqueries';
	
Include **mediaQuery.js** into your html file.
	
	<script src="mediaQuery.js"></script>

Alternatively you can require mediaQuery.js with AMD.

	require(['lib/browser/mediaQuery'], function ( mediaQuery ) {})


## Usage SCSS

### Set up your breakpoints

		$breakpoints: (
  			"mobile"              : "only screen and (max-width:740px)",
  			"tablet"              : "only screen and (max-width:1050px)",
  			"desktop"             : "only screen and (min-width:1051px)",
  			"print"               : "print"
		);
		
### use the magic 
		
		body {
			padding: 40px;
		}
		
		@include breakpoint(tablet) {
			body {
				padding: 20px;
			}
		}
		
		.main {
			margin: 40px;
			@include breakpoint(mobile) {
				margin: 20px;
			}
		}
		


## Usage JS

    // mediaQuery.onEnter / onLeave (querryString,callback,callOnRegister)

    mediaQuery.onEnter('mobile tablet', function(querry){
      console.log(querry);
    },true);

    mediaQuery.onLeave('mobile', function(querry){
      console.log(querry);
    },true);

    if ( mediaQuery.is('mobile') ){
      console.log('I'm a mobile)
    }

    if ( mediaQuery.isNot('mobile') ){
      console.log('I'm a mobile)
    }

## Grid !Optional
`_grid.scss` can be included optionally. `@import 'grid';` and called like this: `@include sensibleGrid()`

 It provides a lightweight, flexible and responsive grid based on sensible. The classes generated by it will look like this:

	.l-one-whole, .l-one-half, .l-one-quarter, .l-mobile-one-whole, .l-mobile-one-half, .l-mobile-one-quarter

then best thing is, that they work like you would expect to: 

	.l-one-whole { width: 100% }
	.l-one-half { width: 50% }
	//etc..

You can use is with the classes listed here fully configure it:

	@include sensibleGrid (
    	$modern: false, // flex-box or inline-block
    	$gutter: 20px,	// gutter between the col's
    	$base-font-size: 16px, // base-font-size only used for inline-block layout
    	$slug: "l-", // slug used for generated classes
    	$pushClasses: false, // do you need .l-push-one-quarter etc. classes ?
    	$gridWidths: ( // grid withs and names
        	"one-whole"         : 100%,
        	"one-half"          : 50%,
        	"one-quarter"       : 25%,
        	"three-quarters"    : 75%,
        	"one-third"         : 33.333%,
        	"two-thirds"        : 66.666%,
        	"one-fifth"         : 20%,
        	"four-fifths"       : 80%,
        	"one-sixth"         : 16.666%,
        	"five-sixths"       : 83.333%
    	),
    	$gridBreakpoints: "mobile-portrait" "mobile" "not-mobile" "tablet-portrait" "tablet" "not-tablet"  "print" //only include the breakpoints you use here to avoid a bloated css
	)
