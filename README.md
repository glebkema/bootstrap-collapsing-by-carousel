# Bootstrap 3. Collapse and expand blocks under the&nbsp;carousel depending on&nbsp;the&nbsp;active&nbsp;slide

Add the class `for-slide-2` to&nbsp;the&nbsp;block, and&nbsp;the&nbsp;block will&nbsp;be&nbsp;expanded under the&nbsp;slide with&nbsp;the&nbsp;index&nbsp;`2`. 

The block can respond to a few slides. The slide can control multiple blocks.

In contrast to the [Accordion example](http://getbootstrap.com/javascript/#collapse-example-accordion), the&nbsp;blocks are always expanded in&nbsp;only&nbsp;one direction&nbsp;&ndash; from&nbsp;top to&nbsp;bottom.

![Screenshot](https://github.com/glebkema/bootstrap-collapsing-by-carousel/blob/master/bootstrap-collapsing-by-carousel.png)

## HTML

```html
<div class="container">
  <div id="myCarousel" class="carousel slide" data-ride="carousel">
    <!-- Indicators -->
    <ol class="carousel-indicators">
      <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
      <li data-target="#myCarousel" data-slide-to="1"></li>
      <li data-target="#myCarousel" data-slide-to="2"></li>
      <li data-target="#myCarousel" data-slide-to="3"></li>
      <li data-target="#myCarousel" data-slide-to="4"></li>
    </ol>

    <!-- Wrapper for slides -->
    <div class="carousel-inner" role="listbox">
      <div class="item active">
        <img class="img-responsive" src="http://placehold.it/1920x650&amp;text=Slide%200" alt="Slide 0">
        <div class="carousel-caption">
          <h3>Caption 0</h3>
        </div>
      </div>
      <div class="item">
        <img class="img-responsive" src="http://placehold.it/1920x650&amp;text=Slide%201" alt="Slide 1">
        <div class="carousel-caption">
          <h3>Caption 1</h3>
        </div>
      </div>
      <div class="item">
        <img class="img-responsive" src="http://placehold.it/1920x650&amp;text=Slide%202" alt="Slide 2">
        <div class="carousel-caption">
          <h3>Caption 2</h3>
        </div>
      </div>
      <div class="item">
        <img class="img-responsive" src="http://placehold.it/1920x650&amp;text=Slide%203" alt="Slide 3">
        <div class="carousel-caption">
          <h3>Caption 3</h3>
        </div>
      </div>
      <div class="item">
        <img class="img-responsive" src="http://placehold.it/1920x650&amp;text=Slide%204" alt="Slide 4">
        <div class="carousel-caption">
          <h3>Caption 4</h3>
        </div>
      </div>
    </div>

    <!-- Controls -->
    <a class="left carousel-control" href="#myCarousel" role="button" data-slide="prev">
      <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="right carousel-control" href="#myCarousel" role="button" data-slide="next">
      <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>

  <div id="collapseGroup">
    <div class="collapse for-slide-0">
      <div class="well">
        <h3>Text for slide 0</h3>
      </div>
    </div>
    <div class="collapse for-slide-1 for-slide-3">
      <div class="well">
        <h3>Text for slides 1 and 3</h3>
      </div>
    </div>
    <div class="collapse for-slide-0 for-slide-2">
      <div class="well">
        <h3>Text for slides 0 and 2</h3>
      </div>
    </div>
    <div class="collapse for-slide-0 for-slide-1 for-slide-2">
      <div class="well">
        <h3>Text for slides 0, 1 and 2</h3>
      </div>
    </div>
  </div>
</div>
```

## Javascript

```javascript
$( document ).ready(function() {
  var CLASS_CAROUSEL    = '#myCarousel';
  var CLASS_FOR_SLIDE   = '.for-slide-';
  var CLASS_GROUP       = '#collapseGroup';
  
  var CLASS_COLLAPSE    = CLASS_GROUP + '>.collapse';
  var CLASS_COLLAPSE_IN = CLASS_COLLAPSE + '.in';

  var selectGroup       = $(CLASS_GROUP); 
  var selectCarousel    = $(CLASS_CAROUSEL);

  // Expand blocks for the slide with index zero.
  $(CLASS_FOR_SLIDE + 0).collapse('show').appendTo(selectGroup);
    
  selectCarousel.on('slide.bs.carousel', function (e) {
    var classTarget  = CLASS_FOR_SLIDE + $(e.relatedTarget).index();
    var selectTarget = $(classTarget);
    
    if ( selectTarget.hasClass('in') ) {
      // Collapse the part of expanded blocks, expand the part of collapsed ones.
      // These two lines are not necessary if each slide controls only one block.
      $(CLASS_COLLAPSE_IN + ':not(' + classTarget + ')').collapse('hide');
      $(CLASS_COLLAPSE + classTarget + ':not(.in)').collapse('show');
    } else {
      // Collapse all expanded blocks and expand new ones.
      $(CLASS_COLLAPSE_IN).collapse('hide');
      selectTarget.collapse('show');
    }
  });
  
  selectCarousel.on('slid.bs.carousel', function (e) {
    // The expanding of a new block will look like a movement from top to bottom,
    // only if old expanded blocks will be placed after it in the DOM.
    $(CLASS_COLLAPSE_IN).appendTo(selectGroup);
  });
});
```

## Required

* jQuery 
* bootstrap.min.js (or set of [transition.js](http://getbootstrap.com/javascript/#transitions), [collapse.js](http://getbootstrap.com/javascript/#collapse) and [carousel.js](http://getbootstrap.com/javascript/#carousel))
* bootstrap.min.css

Look [Bootstrap's basic template](http://getbootstrap.com/getting-started/#template) and [Bootstrap CDN](http://getbootstrap.com/getting-started/#download-cdn).

## Demo

* [Codepen](http://codepen.io/glebkema/pen/PNrBbX)
* [Bootply](http://www.bootply.com/0yR7QTvNNw)

## Thanks

* [Stack Overflow](http://stackoverflow.com/questions/37265371/#37277437)
