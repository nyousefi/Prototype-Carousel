# Prototype Carousel

Original code by Victor Stanciu
Original project url: http://code.google.com/p/prototype-carousel/

## Description

Carousel is a highly configurable Prototype.js extension that creates a nice way of presenting content that is logically broken into several pieces / steps / etc. It's:

* Lightweight - 12 KB
* Cross-browser - Tested on Internet Explorer 6/7/8, Firefox 2/3, Google Chrome, Opera 9.64

## Modifications of the Original Code

This version features customizable button disabling when you're at the first and last slide, and a new type of transition animation called "phase".

## Examples

Available at http://dev.victorstanciu.ro/prototype/carousel/

## Requirements

Carousel.js needs both the Prototype JavaScript framework and the Script.aculo.us effects library to work.

## Usage

* Download carousel.js or carousel-min.js
* Include the script in your page, after the Prototype and Script.aculo.us libraries:
	
	<script type="text/javascript" src="prototype.js"></script>
	<script type="text/javascript" src="scriptaculous.js"></script>
	<script type="text/javascript" src="carousel.js"></script>

### Markup

The minimum markup is:

	<div id="carousel-wrapper">
	    <div id="carousel-content">
	        <div class="slide"></div>
	        <div class="slide"></div>
	        ...
	        <div class="slide"></div>
	    </div>
	</div>

And the minimum styling is:

	#carousel-wrapper {
	    width: 500px;
	    height: 500px;
	    overflow: hidden;
	}
	#carousel-content {
	    width: 2500px; /* should be the total space needed for all slides */
	}
	#carousel-content .slide {
	    float: left;
	    width: 500px;
	    height: 500px;
	}
	.control-dead {
		visibility: hidden; /* hides inactive controls */
	}

This will generate a 500x500px Carousel with horizontal movement. Switching to vertical movement is as simple as setting #carousel-content's width to 500px, the width of a single slide.

### Initialization

You initialize the Carousel by: 

	new Carousel(wrapper, slides, triggers, {options});
	
Example for the markup above:

	new Carousel('carousel-wrapper', $$('#carousel-content .slide'), $$('#carousel-content a.carousel-control', '#carousel-content a.carousel-jumper'));

### Triggers

There are two categories of elements that trigger the carousel's movement: the ones that trigger a direct jump to a selected slide (jump to slide "x"), and the ones that start a relative jump (jump to first/last/previous/next slide). The combination of a trigger's rel and class attributes decide the Carousel's behavior. For example, clicking on:

	<a href="javascript:" class="carousel-jumper" rel="slide-1">Jump to slide 1</a>

Will jump to the slide that has the id "slide-1". And:

	<a href="javascript:" class="carousel-control" rel="prev">Previous slide</a>

Will jump to the previous slide. Available options for the `rel` attribute are `first`, `last`, `prev` and `next`.

### Using Multiple Carousels on the Same Page

You can use multiple carousels on the same page. Simply give each carousel its own id names.
	
	new Carousel('carousel-1', $$('#carousel-1-content .slide'), $$('#carousel-1-content a.carousel-control', '#carousel-1-content a.carousel-jumper'));
	
	new Carousel('carousel-2', $$('#carousel-2-content .slide'), $$('#carousel-2-content a.carousel-control', '#carousel-2-content a.carousel-jumper'));
	
A common mistake is to only use `a.carousel-control` in the initializers, which causes any one control to change all the slides on the page. (Of course, if that's your goal go ahead and do that.)

## Available Options

Options are given as the last parameter in the initialization as hash: {option: value, option: value}

<table>
  <tr>
    <td><strong>Options</strong></td>
    <td><strong>Default</strong></td>
    <td><strong>Description</strong></td>
  </tr>
  <tr>
    <td>duration</td>
    <td>1</td>
    <td>The duration of a full jump</td>
  </tr>
  <tr>
    <td>auto</td>
    <td>false</td>
    <td>When <strong>true</strong> the Carousel will move on it's own without needing triggers. Useful for slideshows</td>
  </tr>
  <tr>
    <td>frequency</td>
    <td>3</td>
    <td>When <strong>auto</strong> is <strong>true</strong>, this dictates how long a slides stays put before the next jump</td>
  </tr>
  <tr>
    <td>visibleSlides</td>
    <td>1</td>
    <td>Even though multiple slides can be made visible at once by styling, this parameters is needed in some calculations</td>
  </tr>
  <tr>
    <td>circular</td>
    <td>false</td>
    <td>By default when the first/last slide is reached, calling <strong>prev</strong>/<strong>next</strong> does nothing. If you want the effect to continue, you must do two things: Set the <strong>circular</strong> parameter <strong>true</strong> and <strong>duplicate</strong> the <strong>first</strong> slide in the HTML. It's the only way of giving the impression of a continous movement.</td>
  </tr>
  <tr>
    <td>wheel</td>
    <td>true</td>
    <td>Whether or not to slide when using the mouse wheel over the slides</td>
  </tr>
  <tr>
    <td>effect</td>
    <td>scroll</td>
    <td>You can choose between <strong>scroll</strong>, <strong>fade</strong>, and <strong>phase</strong>. When using <strong>fade</strong>, <strong>circular</strong> and duplicating the first slide is no longer necessary (see <a href="http://dev.victorstanciu.ro/prototype/carousel/" rel="nofollow">Example 3</a> for the <strong>fade</strong> effect). <strong>Phase</strong> combines the scroll and fade effects: the slide fades out, scrolls, and the new slide fades in. When using the <strong>phase</strong> effect you can use the <strong>phaseOpacity</strong> and <strong>phaseDuration</strong> options.</td>
  </tr>
	<tr>
		<td>phaseDuration</td>
		<td>0.5</td>
		<td>The length of time it takes to complete the fade when the phase effect is being used. Ignored if other effects are used.</td>
	</tr>
	<tr>
		<td>phaseOpacity</td>
		<td>0.3</td>
		<td>The lightest opacity of the slides during the phase effect.</td>
	</tr>
  <tr>
    <td>transition</td>
    <td>sinoidal</td>
    <td>The three supported transitions are <strong>sinoidal</strong> and <strong>spring</strong> (see <a href="http://dev.victorstanciu.ro/prototype/carousel/" rel="nofollow">Example 2</a> for <strong>spring</strong>)>.</td>
  </tr>
  <tr>
    <td>selectedClassName</td>
    <td>carousel-selected</td>
    <td>When triggering a jump by using a <strong>carousel-jumper</strong> trigger (jumps to specified slide), this CSS class is added to the trigger, to help you in visually highlighting it (see <a href="http://dev.victorstanciu.ro/prototype/carousel/" rel="nofollow">Examples</a> for tab-navigation example)</td>
  </tr>
  <tr>
    <td>beforeMove</td>
    <td>null</td>
    <td>User function that will be executed before a jump is started. For example: {beforeMove: function () { alert("Here i go!"); }}</td>
  </tr>
  <tr>
    <td>afterMove</td>
    <td>null</td>
    <td>Just like <strong>beforeMove</strong>, only it's called after the move is completed.</td>
  </tr>
</table>


