Visualz++ - Make your image flashy!
==============================
*JQuery-based script for audio visualization*
______________________________
Introduction
------------------------------
Based on original [Visualz](https://github.com/Juribiyan/visualz), this script provides hover and audio visualization.
_____________________________
Differences from original 
------------------------------
* Easier to install - download and put where you want. All scripts and styles are present. No need to get your hands dirty...
* ...Unless you want to personalize it a bit! Do follow steps in customization section and everything will be fine!
* Some extra presets added.
* Some annoying errors fixed.
* Added proper documentation! 
______________________________
Requirements
------------------------------
* JQuery, at least 1.11.1.
* A png.-image (Other formats aren't tested yet)
* A couple of hands to play with customization.
* A couple of eyes to read the manual.
_____________________________
Installation guide
------------------------------
#### Getting image ready
Choose the picture you desire and put it to */img* folder. **Do not** resize it through CSS or visualization will go nuts.

#### Making pic flash
When you have the image, insert it into HTMLt. Don't forget to give it an ID.

Now, in the CSS-file, make sure to position the image right. Make sure that ```.cell-grid, .grid-wrap img``` have the same positioning parameters. And don't forget to insert ```.cell```, ```.cell-hover``` and ```.grid-wrap``` into your CSS. Check *style.css* for more information.

The following method should be called when you're done:

```javascript
$('#image').visualize(preset)
```
Where ```#image``` is the id you gave it in the HTML-document.

This method creates visualization container based on the image you've provided. 
> Do note that image should be loaded *before* the method is called. You can use e.g.```$document.ready()``` for that.

If you did everything right, visualization should work when you hover your mouse over the image.

#### Adding some music
Go ahead and put some tracks to */loop* folder. 
> Do note that for better compatibility it's good to have the same track in both *.mp3* and *.ogg*.  

Create an ```<audio>```-element in your HTML, give it an ID. Then, inside the script area, create variable ```playlist```. It should contain an array with your track names. If you're not using both *.mp3* and *.ogg*, do write audio extension. The array may look like this:

```Javascript
var playlist = ["track1", "track2.mp3", "track3.ogg"]
```
In this case, you'll need *track1.mp3, track1.ogg, track2.mp3*, and *track3.ogg* in the *loop* folder. Script will choose one track randomly when page is updated or ```switchTrack()``` is called. 

> Do note that you should update this array manually, when adding or deleting tracks.

When your playlist-array is ready, create audio play/pause element. It can be a link or anything else, give it ID as well. 

Then, define audio controls by calling following method:

``` Javascript
var controls = $('#audio').analyze(playlist)
```
where ```#audio``` is the ID you gave to your audio element and ```controls``` is the ID you gave to controlling element.

Now make this controller work using ```playPause()```-method e.g. like this:

```Javascript
$('#controls').on('click',function () {
    controls.playPause();
});
```
If you want to switch tracks on click, you can add ```controls.switchTrack();``` below ```playPause()```. 

If you did everything right, your pic should now flash when you hover your pointer over it or when music plays.
______________________________

Customization
------------------------------
#### Presets
##### Usage

```preset``` defines the pattern of the cells. In ```visualize(preset)```, it may contain a name of a built-in preset or an object with visualization settings. If no preset is defined, random built-in preset will be chosen. 

##### Preset formatting
```cw``` - cell width in pixels.
```ch``` — cell height in pixels.
Both also support ```100%``` to extend the cell across the whole image.   
css — extra CSS for the cell.
##### Adding new preset
You may add presets through calling  ```$.addPreset(name, preset)``` *before* ```visualize()``` is called.  You may also add presets directly to visuals.js under ```var presets```.

#### Color of the cells
If you want to alter the color of the canvas, go to visuals.js go to ```getBrightenImg(img)```-function. Find the following code: 

```Javascript
    for (var i = 0; i < d.length; i += 4) {
      d[i] = 195 //Red
      d[i + 1] = 255 //Green
      d[i + 2] = 252 //Blue
    }
```

This code generates the pixels using RGB-format. You can change the values from 0 to 255. Use color picker if you're unsure.
#### CSS customization
You can customize opacity of ```.cell-hover```. That will define how "bright" the flash will be. You can also customize ```transition-duration``` of ```.cell``` to set the duration of cell switching between visible and invisible.

______________________________
Known issues
------------------------------
* Visualization works weird if original image was changed through CSS.
* Will lag on mobile devices.
* Gives a couple of "Deprecation" warnings in Chrome. 
* May not work locally due to CORS error. Test it on localhost.
______________________________
To Do
------------------------------
* Fix deprecation warnings in Chrome
* Preset switch function
* Translate this document to Swedish and Russian
* Add more presets(?)
* Anything else? Let me know. 