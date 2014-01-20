---
layout: post
category : Letters
tags : [menlo, study]
---
#Loading Time Perception
##An open letter to [Menlo Innovations]
=========

I recently noticed that the your main site loaded slower then expected. When I looked at where most of the load time was going I noticed that your background image was rather large. I posted a quick note about it on your facebook page on Friday night and you had resized the image and replied to my post by Sunday.

I was impressed that you guys took notice and took action to change it so quickly.

When I went back to check on the page the load time was reduced but I realized the real problem wasn't just that the image was large. It was that it loaded in **visibly** slowly. I also noticed that while the backgrounds on all your other pages were 1920x1200 the new resized image was 1680×1050. The reduced size had presented black bars on the side of the page.

####Slow Background loading
![Alt text](/files/expand_arrow.JPG "Image call example")  

####Undesirable Borders  
![Alt text](/files/expand_arrow.JPG "Image call example")  

To fix the background border issue you can move the background tag out of the body into it's own styled div:

###old html
```html
<body id="homepage" onload="javascript:headerLinks(document.location.href);" style="background:#000000 url('img/bkgrd/collage-2014-01.jpg') no-repeat fixed center top"> 
```

###new html
```html
<body id="homepage" onload="javascript:headerLinks(document.location.href);"  style="background:#111111" > 
<div id="bg">
  <img src="img/bkgrd/collage-2014-01.jpg" alt="">
</div>
```

###css
```css
#bg {
  position: fixed; 
  top: -50%; 
  left: -50%; 
  width: 200%; 
  height: 200%;
}

#bg img {
  position: absolute; 
  top: 0; 
  left: 0; 
  right: 0; 
  bottom: 0; 
  margin: auto; 
  min-width: 50%;
  min-height: 50%;
}
```
This creates a nice static background that remains static independent of resolution
####Before
![Alt text](/files/expand_arrow.JPG "Image call example")    
####After
![Alt text](/files/expand_arrow.JPG "Image call example")    
   
The background popping in can be fixed by having the image load in the background and after it's fully loaded, have it fade it in.
```js
    $(window).load(function(){
    $('<img/>').attr('src', 'img/bkgrd/collage-2014-01.jpg').load(function() {          
    	    $('#bg').fadeIn(200); //200 ms fade in time
		});
	});
```

But we have to set the background to initially not be shown (style="display:none").
```html
<div id="bg" style="display:none">
  <img src="img/bkgrd/collage-2014-01.jpg" alt="">
</div>
```
####Before
![Alt text](/files/expand_arrow.JPG "Image call example")    
####After
![Alt text](/files/expand_arrow.JPG "Image call example")

As a note, that javascript as it is would have to be added to each page. It could be placed into an anonymous function that can be passed the background image as a parameter and loaded via a script tag. That way if you have to change the transition time for the background you can do it from a single place.

I hope this helps. Of course this is a bit more work but it makes a world of difference for the experience. Contact me if you need any details.

[Menlo Innovations]:http://www.menloinnovations.com/
