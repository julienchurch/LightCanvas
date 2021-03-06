# LightFX 

LightFX is a small library for adding canvas-based UI effects. It is not a canvas manipulation library like FabricJS; instead it offers a handful of things I've always been unsatisfied with in native CSS.

Since it grew as a need-based, organic library of functions LightFX is very specific, and allows you to easily:

* Add extremely-efficient gaussian-like blurs
* Animate those blurs in and out
* Adjust lightness
* Adjust contrast
* Adjust saturation

## Why not just do this with CSS?

Well, there are a few reasons. 

First, animating blurs with CSS/SVG tends to be unpredictable. I've noticed what is, for lack of a better term, a "bounce": the blurring animation seemed to jump around is if were dropping frames at high speed. In the project that spawned this project, I was looking for a smooth, native-style blur. CSS just wasn't offering that.

Second, it also resolves the edge issue: when you blur an image with CSS, the alpha channel along the edges decreases as the edge feathers with the blur. This means the colors around the edge bleed in ways that aren't pretty and require unpleasant hacks to deal with.

## Using LightFX 

**Note:** If you're not running this code through the a server, your browser will complain about cross origin requests. In Chrome you can override this security measure with the command 

    open -a 'Google Chrome' --args -allow-file-access-from-files

I don't particularly recommend this. Instead, I prefer to run a simple Python server:

    cd examples
    python -m SimpleHTTPServer

This will satisfy the same origin policy, allowing canvas access to the example files in this repository. Just navigate to `localhost:8000` (or whatever port is listed in your console) in your browser and you're golden. 

### Example

Let's add an image and create a LightFX object.

```js
var img = document.getElementById("image");
var lfx = new LightFX(img);
```

This duplicates the image into a canvas of the same dimensions. From here, transforming is easy:

```js
lfx.lightblur(75); // 75 pixel radius pseudo-gassian blur based on stackblur
```

Boom. Done. You blurred it. How about lightness?

```js
lfx.lightness(100); // range from -255 to +255
```

Now your canvas image is lighter. (Whoa!)

Of course, to actually *view* this change, you'll have to append `lfx.canvas` somewhere in the body of your document.

## Mini-documentation

Here are the currently-available methods on a LightFX object

**stackblur(radius)**  
Run the highly-efficient stackblur algorithm over the canvas  

**lightblur(radius)**  
Run the even-more-highly-efficient lightblur algorithm over the canvas  

**lightness(lightnessValue)**   
Increase or decrease lightness linearly (accepts range -255 to +255)  

**contrast(contrastValue)**  
Increase or decrase contrast (accepts range -100 to +100)  

**saturation(saturationValue)**  
Increase or decrase saturation (accepts range -255 to +255)

**blurIn(framerate, radius)**  
Use the lightblur algorithm to animate a blurring in of the image to the specified radius

**blurOut(framerate, radius)**  
Use the lightblur algorithm to animate a blurring out of the the image from the specified radius

## More to come

Stay tuned
