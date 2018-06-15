# Retina-Resposive-image-layout
Retina display and responsive image with flexbox layout 
## Retina displays and mobile devices complicate things
To make our images responsive, we now have to take three things into consideration:

   - The device’s dimensions
   - The image’s dimensions
   - The device’s screen resolution

Retina screens have twice as many pixels per inch than standard-resolution screens. That is to say, each retina pixel is the equivalent of 4 standard pixels.
Standard displays and smaller devices don’t need all those extra pixels in high-resolution images, and sending that much unnecessary data usually results in a bad user experience.
SVGs avoid the screen resolution problems, Browsers automatically scale up SVGs for retina devices.
```
<div class='section content'>
  <img class='illustration' src='images/illustration.svg' />
</div>
```
```
.illustration {
  width: 100%;
}
```
We want to cap the width of the illustration to its inherent width, which is 500 pixels. We can do this with an inline style:
```
<div class='section content'>
  <img class='illustration' src='images/illustration.svg' style='max-width: 500px'/>
</div>
```
If you’re not worried about optimization, responsive raster images really aren’t that much harder than using SVG images. Try swapping out our existing illustration.svg with a PNG file:
```
<div class='section content'>
  <div class='illustration'>
    <img src='images/illustration-big.png' style='max-width: 500px'/>
  </div>
</div>
```
We changed around the HTML structure a bit, nesting our <img/> tag in another container. Without it, the image would get distorted because flexbox would try to set its height to be the same as the .content container. This requires a little tweak to our .illustration CSS rule, too:
```
.illustration img {
  width: 100%;
  display: block;
}
```
High-resolution images are big. Our illustration-big.png file takes up more than twice as much disk space as its low-resolution counterpart. It doesn’t make sense to serve all that extra data when the user doesn’t actually need it.

Adding a srcset attribute to our <img/> element lets us present our high-resolution image only to retina devices, falling back to the low-resolution version for standard screens. Update our .illustration element to match the following:
```
<div class='illustration'>
  <img src='illustration-small.png'
       srcset='images/illustration-small.png 1x,
               images/illustration-big.png 2x'
       style='max-width: 500px'/>
</div>
```
```
<div class='section header'>
  <div class='photo'>
    <img src='images/photo-small.jpg'
         srcset='images/photo-big.jpg 2000w,
                 images/photo-small.jpg 1000w'
         sizes='(min-width: 960px) 960px,
                100vw'/>
  </div>
</div>
```
Add both of the following rules to our other base styles, right above the mobile styles media query:
```
.header {
  height: auto;
  justify-content: inherit;
  align-items: inherit;
}

.photo img {
  width: 100%;
  display: block;
}
```
