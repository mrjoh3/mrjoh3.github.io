---
title: Shiny Image Gallery Examples
author: Matt Johnson
date: '2018-12-26'
slug: shiny-image-gallery-examples
image: 'img/MRJ_2020_DSC9961.png'
categories:
  - web
tags:
  - shiny
  - gallery
  - image
  - js
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
draft: true
output:
  html_document:
    keep_md: yes
---

# DRAFT

Some time ago I had to implement an image gallery within a `shiny` application. A simple grid of small thumbnail images where clicking opens the full image.  Nothing complicated, but I did have several requirements:

  1. The gallery needed to render from a folder of images
  2. The gallery interface and thumbnails needed to be responsive
  3. The gallery needed to link to other `shiny` UI
  4. The full-size image should be zoomable to see the full resolution.
  
There is a wide variety of javascript image gallery implementations. To start with I looked at  [Lightbox](https://lokeshdhakar.com/projects/lightbox2/) and [PhotoSwipe](http://photoswipe.com/). Lightbox was the easiest to use and many other JS libraries are based on it. Photoswipe is also very popular with a very nice UI, zoom and touch integration plus an extensive API. Both are available under MIT licences. Unfortunately my javascript is limited and I did not have enough time to get more than the most basic Photoswipe gallery to work. But, the Lightbox gallery works very nicely.

This work was eventually built into a [shiny app](https://mrjoh3.shinyapps.io/shiny-gallery-example/) so you can see the galleries in action. I have also wrapped the code in the [gallerier](https://github.com/mrjoh3/gallerier) package. `Gallerier` can be used in both `shiny` and `rmarkdown` documents. Code for the original `shiny` app is on [Github](https://github.com/mrjoh3/shiny-gallery-example).


## Data Preparation



```r
library(dplyr)
library(lubridate)
library(hashids)
library(gallerier)

images <- data.frame(src = list.files('www/img')) %>%
  tidyr::separate(col = 'src', 
                  c('txt', 'date', 'time', 'msec'), 
                  sep = '_|\\.', 
                  remove = FALSE) %>%
  rowwise() %>%
  mutate(date = lubridate::ymd(date),
         key = hashids::encode(1e3 + as.integer(msec), 
                               hashid_settings(salt = 'this is my salt')))
```

```r
## simple lightbox
lightbox_gallery(images, 
                 'gallery', 
                 display = TRUE)
```



<div style="display: TRUE;">
<div class="card-deck">
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181019_131513_230.jpg" data-lightbox="gallery" data-title="IMG_20181019_131513_230.jpg - IMG - 17823 - 131513 - 230 - Vvm - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181019_131513_230.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181022_160737_185.jpg" data-lightbox="gallery" data-title="IMG_20181022_160737_185.jpg - IMG - 17826 - 160737 - 185 - MQB - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181022_160737_185.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181024_180354_405.jpg" data-lightbox="gallery" data-title="IMG_20181024_180354_405.jpg - IMG - 17828 - 180354 - 405 - rQV - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181024_180354_405.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181024_180354_425.jpg" data-lightbox="gallery" data-title="IMG_20181024_180354_425.jpg - IMG - 17828 - 180354 - 425 - mZR - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181024_180354_425.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181024_180354_432.jpg" data-lightbox="gallery" data-title="IMG_20181024_180354_432.jpg - IMG - 17828 - 180354 - 432 - 3LY - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181024_180354_432.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181024_183858_737.jpg" data-lightbox="gallery" data-title="IMG_20181024_183858_737.jpg - IMG - 17828 - 183858 - 737 - WK4 - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181024_183858_737.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181025_183729_821.jpg" data-lightbox="gallery" data-title="IMG_20181025_183729_821.jpg - IMG - 17829 - 183729 - 821 - opR - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181025_183729_821.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181026_142940_957.jpg" data-lightbox="gallery" data-title="IMG_20181026_142940_957.jpg - IMG - 17830 - 142940 - 957 - xJEy - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181026_142940_957.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181119_172905_259.jpg" data-lightbox="gallery" data-title="IMG_20181119_172905_259.jpg - IMG - 17854 - 172905 - 259 - zMW - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181119_172905_259.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181213_094058_994.jpg" data-lightbox="gallery" data-title="IMG_20181213_094058_994.jpg - IMG - 17878 - 094058 - 994 - laaX - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181213_094058_994.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181215_090527_868.jpg" data-lightbox="gallery" data-title="IMG_20181215_090527_868.jpg - IMG - 17880 - 090527 - 868 - LzX - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181215_090527_868.jpg" width="80px" height="auto"/>
</a>
</div>
<div data-type="template" class="card">
<a id="ef8a6" href="www/img/IMG_20181224_194148_000.jpg" data-lightbox="gallery" data-title="IMG_20181224_194148_000.jpg - IMG - 17889 - 194148 - 000 - 5vJ - ef8a6">
<img class="card-img-top" src="www/img/IMG_20181224_194148_000.jpg" width="80px" height="auto"/>
</a>
</div>
</div>
<script>/*!
 * Lightbox v2.10.0
 * by Lokesh Dhakar
 *
 * More info:
 * http://lokeshdhakar.com/projects/lightbox2/
 *
 * Copyright 2007, 2018 Lokesh Dhakar
 * Released under the MIT license
 * https://github.com/lokesh/lightbox2/blob/master/LICENSE
 *
 * @preserve
 */
!function(a,b){"function"==typeof define&&define.amd?define(["jquery"],b):"object"==typeof exports?module.exports=b(require("jquery")):a.lightbox=b(a.jQuery)}(this,function(a){function b(b){this.album=[],this.currentImageIndex=void 0,this.init(),this.options=a.extend({},this.constructor.defaults),this.option(b)}return b.defaults={albumLabel:"Image %1 of %2",alwaysShowNavOnTouchDevices:!1,fadeDuration:600,fitImagesInViewport:!0,imageFadeDuration:600,positionFromTop:50,resizeDuration:700,showImageNumberLabel:!0,wrapAround:!1,disableScrolling:!1,sanitizeTitle:!1},b.prototype.option=function(b){a.extend(this.options,b)},b.prototype.imageCountLabel=function(a,b){return this.options.albumLabel.replace(/%1/g,a).replace(/%2/g,b)},b.prototype.init=function(){var b=this;a(document).ready(function(){b.enable(),b.build()})},b.prototype.enable=function(){var b=this;a("body").on("click","a[rel^=lightbox], area[rel^=lightbox], a[data-lightbox], area[data-lightbox]",function(c){return b.start(a(c.currentTarget)),!1})},b.prototype.build=function(){if(!(a("#lightbox").length>0)){var b=this;a('<div id="lightboxOverlay" class="lightboxOverlay"></div><div id="lightbox" class="lightbox"><div class="lb-outerContainer"><div class="lb-container"><img class="lb-image" src="data:image/gif;base64,R0lGODlhAQABAIAAAP///wAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==" /><div class="lb-nav"><a class="lb-prev" href="" ></a><a class="lb-next" href="" ></a></div><div class="lb-loader"><a class="lb-cancel"></a></div></div></div><div class="lb-dataContainer"><div class="lb-data"><div class="lb-details"><span class="lb-caption"></span><span class="lb-number"></span></div><div class="lb-closeContainer"><a class="lb-close"></a></div></div></div></div>').appendTo(a("body")),this.$lightbox=a("#lightbox"),this.$overlay=a("#lightboxOverlay"),this.$outerContainer=this.$lightbox.find(".lb-outerContainer"),this.$container=this.$lightbox.find(".lb-container"),this.$image=this.$lightbox.find(".lb-image"),this.$nav=this.$lightbox.find(".lb-nav"),this.containerPadding={top:parseInt(this.$container.css("padding-top"),10),right:parseInt(this.$container.css("padding-right"),10),bottom:parseInt(this.$container.css("padding-bottom"),10),left:parseInt(this.$container.css("padding-left"),10)},this.imageBorderWidth={top:parseInt(this.$image.css("border-top-width"),10),right:parseInt(this.$image.css("border-right-width"),10),bottom:parseInt(this.$image.css("border-bottom-width"),10),left:parseInt(this.$image.css("border-left-width"),10)},this.$overlay.hide().on("click",function(){return b.end(),!1}),this.$lightbox.hide().on("click",function(c){return"lightbox"===a(c.target).attr("id")&&b.end(),!1}),this.$outerContainer.on("click",function(c){return"lightbox"===a(c.target).attr("id")&&b.end(),!1}),this.$lightbox.find(".lb-prev").on("click",function(){return 0===b.currentImageIndex?b.changeImage(b.album.length-1):b.changeImage(b.currentImageIndex-1),!1}),this.$lightbox.find(".lb-next").on("click",function(){return b.currentImageIndex===b.album.length-1?b.changeImage(0):b.changeImage(b.currentImageIndex+1),!1}),this.$nav.on("mousedown",function(a){3===a.which&&(b.$nav.css("pointer-events","none"),b.$lightbox.one("contextmenu",function(){setTimeout(function(){this.$nav.css("pointer-events","auto")}.bind(b),0)}))}),this.$lightbox.find(".lb-loader, .lb-close").on("click",function(){return b.end(),!1})}},b.prototype.start=function(b){function c(a){d.album.push({alt:a.attr("data-alt"),link:a.attr("href"),title:a.attr("data-title")||a.attr("title")})}var d=this,e=a(window);e.on("resize",a.proxy(this.sizeOverlay,this)),a("select, object, embed").css({visibility:"hidden"}),this.sizeOverlay(),this.album=[];var f,g=0,h=b.attr("data-lightbox");if(h){f=a(b.prop("tagName")+'[data-lightbox="'+h+'"]');for(var i=0;i<f.length;i=++i)c(a(f[i])),f[i]===b[0]&&(g=i)}else if("lightbox"===b.attr("rel"))c(b);else{f=a(b.prop("tagName")+'[rel="'+b.attr("rel")+'"]');for(var j=0;j<f.length;j=++j)c(a(f[j])),f[j]===b[0]&&(g=j)}var k=e.scrollTop()+this.options.positionFromTop,l=e.scrollLeft();this.$lightbox.css({top:k+"px",left:l+"px"}).fadeIn(this.options.fadeDuration),this.options.disableScrolling&&a("html").addClass("lb-disable-scrolling"),this.changeImage(g)},b.prototype.changeImage=function(b){var c=this;this.disableKeyboardNav();var d=this.$lightbox.find(".lb-image");this.$overlay.fadeIn(this.options.fadeDuration),a(".lb-loader").fadeIn("slow"),this.$lightbox.find(".lb-image, .lb-nav, .lb-prev, .lb-next, .lb-dataContainer, .lb-numbers, .lb-caption").hide(),this.$outerContainer.addClass("animating");var e=new Image;e.onload=function(){var f,g,h,i,j,k;d.attr({alt:c.album[b].alt,src:c.album[b].link}),a(e),d.width(e.width),d.height(e.height),c.options.fitImagesInViewport&&(k=a(window).width(),j=a(window).height(),i=k-c.containerPadding.left-c.containerPadding.right-c.imageBorderWidth.left-c.imageBorderWidth.right-20,h=j-c.containerPadding.top-c.containerPadding.bottom-c.imageBorderWidth.top-c.imageBorderWidth.bottom-120,c.options.maxWidth&&c.options.maxWidth<i&&(i=c.options.maxWidth),c.options.maxHeight&&c.options.maxHeight<i&&(h=c.options.maxHeight),(e.width>i||e.height>h)&&(e.width/i>e.height/h?(g=i,f=parseInt(e.height/(e.width/g),10),d.width(g),d.height(f)):(f=h,g=parseInt(e.width/(e.height/f),10),d.width(g),d.height(f)))),c.sizeContainer(d.width(),d.height())},e.src=this.album[b].link,this.currentImageIndex=b},b.prototype.sizeOverlay=function(){this.$overlay.width(a(document).width()).height(a(document).height())},b.prototype.sizeContainer=function(a,b){function c(){d.$lightbox.find(".lb-dataContainer").width(g),d.$lightbox.find(".lb-prevLink").height(h),d.$lightbox.find(".lb-nextLink").height(h),d.showImage()}var d=this,e=this.$outerContainer.outerWidth(),f=this.$outerContainer.outerHeight(),g=a+this.containerPadding.left+this.containerPadding.right+this.imageBorderWidth.left+this.imageBorderWidth.right,h=b+this.containerPadding.top+this.containerPadding.bottom+this.imageBorderWidth.top+this.imageBorderWidth.bottom;e!==g||f!==h?this.$outerContainer.animate({width:g,height:h},this.options.resizeDuration,"swing",function(){c()}):c()},b.prototype.showImage=function(){this.$lightbox.find(".lb-loader").stop(!0).hide(),this.$lightbox.find(".lb-image").fadeIn(this.options.imageFadeDuration),this.updateNav(),this.updateDetails(),this.preloadNeighboringImages(),this.enableKeyboardNav()},b.prototype.updateNav=function(){var a=!1;try{document.createEvent("TouchEvent"),a=!!this.options.alwaysShowNavOnTouchDevices}catch(a){}this.$lightbox.find(".lb-nav").show(),this.album.length>1&&(this.options.wrapAround?(a&&this.$lightbox.find(".lb-prev, .lb-next").css("opacity","1"),this.$lightbox.find(".lb-prev, .lb-next").show()):(this.currentImageIndex>0&&(this.$lightbox.find(".lb-prev").show(),a&&this.$lightbox.find(".lb-prev").css("opacity","1")),this.currentImageIndex<this.album.length-1&&(this.$lightbox.find(".lb-next").show(),a&&this.$lightbox.find(".lb-next").css("opacity","1"))))},b.prototype.updateDetails=function(){var b=this;if(void 0!==this.album[this.currentImageIndex].title&&""!==this.album[this.currentImageIndex].title){var c=this.$lightbox.find(".lb-caption");this.options.sanitizeTitle?c.text(this.album[this.currentImageIndex].title):c.html(this.album[this.currentImageIndex].title),c.fadeIn("fast").find("a").on("click",function(b){void 0!==a(this).attr("target")?window.open(a(this).attr("href"),a(this).attr("target")):location.href=a(this).attr("href")})}if(this.album.length>1&&this.options.showImageNumberLabel){var d=this.imageCountLabel(this.currentImageIndex+1,this.album.length);this.$lightbox.find(".lb-number").text(d).fadeIn("fast")}else this.$lightbox.find(".lb-number").hide();this.$outerContainer.removeClass("animating"),this.$lightbox.find(".lb-dataContainer").fadeIn(this.options.resizeDuration,function(){return b.sizeOverlay()})},b.prototype.preloadNeighboringImages=function(){if(this.album.length>this.currentImageIndex+1){(new Image).src=this.album[this.currentImageIndex+1].link}if(this.currentImageIndex>0){(new Image).src=this.album[this.currentImageIndex-1].link}},b.prototype.enableKeyboardNav=function(){a(document).on("keyup.keyboard",a.proxy(this.keyboardAction,this))},b.prototype.disableKeyboardNav=function(){a(document).off(".keyboard")},b.prototype.keyboardAction=function(a){var b=a.keyCode,c=String.fromCharCode(b).toLowerCase();27===b||c.match(/x|o|c/)?this.end():"p"===c||37===b?0!==this.currentImageIndex?this.changeImage(this.currentImageIndex-1):this.options.wrapAround&&this.album.length>1&&this.changeImage(this.album.length-1):"n"!==c&&39!==b||(this.currentImageIndex!==this.album.length-1?this.changeImage(this.currentImageIndex+1):this.options.wrapAround&&this.album.length>1&&this.changeImage(0))},b.prototype.end=function(){this.disableKeyboardNav(),a(window).off("resize",this.sizeOverlay),this.$lightbox.fadeOut(this.options.fadeDuration),this.$overlay.fadeOut(this.options.fadeDuration),a("select, object, embed").css({visibility:"visible"}),this.options.disableScrolling&&a("html").removeClass("lb-disable-scrolling")},new b});
//# sourceMappingURL=lightbox.min.map</script>
<style type="text/css">

.card-deck {
  display: flex;
  justify-content: flex-start;
  flex-flow: row wrap;
  align-items: stretch;
  padding: 20px;
  border-spacing: 1.25rem 0;
}
.card-deck .card {
  /*display: block;*/
  flex-basis: 21%; /* change this value for each breakpoint*/
}
.card {
    font-size: 1em;
    overflow: hidden;
    margin: 20px;
    padding: 0;
    border: none;
    border-radius: .28571429rem;
    box-shadow: 0 1px 3px 0 #d4d4d5, 0 0 0 1px #d4d4d5;
    @media(min-width: 56rem) {
      width: 22.3333%;
    }
}

.card-block {
    font-size: 1em;
    position: relative;
    margin: 0;
    padding: 1em;
    border: none;
    border-top: 1px solid rgba(34, 36, 38, .1);
    box-shadow: none;
}

.card-img-top {
    display: block;
    width: 100%;
    height: auto;
}</style>
</div>

