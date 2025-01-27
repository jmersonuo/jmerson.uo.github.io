<h2 align="center"> Part A. Sound and Alt Text</h2>

For this exercise, we will be adding sound to marker popups in a Mapbox map:
  - in popups using an iframe to share a video via absolute link (on the web)
  - in a popup to share a sound file via a relative location (on your computer)
  - adding alt-text descriptions to images
  - linking a Google font and applying it via css
  
We will discuss the use of sounds in detail and how to access the embedded links in more detail in the upcoming "sound" lecture.

  Here are some additional resources you can explore:
  - [W3Schools iframes](https://www.w3schools.com/tags/tag_iframe.asp){:target="_blank"} 
  - [W3Schools image alt attribute](https://www.w3schools.com/tags/att_img_alt.asp){:target="_blank"} 
  - [W3Schools audio tag](https://www.w3schools.com/tags/tag_audio.asp){:target="_blank"} 

----------

### I. Getting setup  

1. From the course R Drive (R:\...Class_Data\Assignment6), download the files to your R drive or local computer. It contains:
  - QickStartMap-withSound.html
  - The folder "Sounds", which contains the file yell-YELLBisonEating150313.mp3 'Source: NPS/Neal Herbert, <a href="https://www.nps.gov/yell/learn/photosmultimedia/sounds-bisoneating.htm" target='_blank'>NPS</a>'

2. Review the HTML. Notice it has the standard:
  - `<head> ... </head>` 
  - `<style> ... </style>`   (nested within the head)
  - `<body> ... </body>` 
  - `<script> ... </script>`  (nested within the body

  When you open the map, and add your Mapbox access token, you should have a mapbox-outdoor style centered on Portland.  
  <p align="center">
    <img src= "Images/6-PortlandOutdoors.JPG"> 
  </p>

----------

### II. Add 3 markers

Let's start by adding 3 markers. Locate the comment `/***  MARKERS  ***/` then add the code block below. Notice that each marker:
  - was set to the color `darkRed`
  - has a Lng/Lat set
  - then is added to the map with the variable named `map`

  ```javascript
   /***  MARKERS  ***/
      // Marker 1 - Portland
     var marker1 = new mapboxgl.Marker({color:'DarkRed'})
        .setLngLat([-122.6788,45.5212]) // Portland 
	   //add .setPopup here
        .addTo(map);

        
    // Marker 2 - London 
    var marker2 = new mapboxgl.Marker({color:'DarkRed'})
       .setLngLat([-0.1534307, 51.501223]) // London 
       .addTo(map);

        
    // Marker 3 - Yellowstone
    var marker3 = new mapboxgl.Marker({color:'DarkRed'})
      .setLngLat([-110.74524187568,44.706216445069]) // Yellowstone
      .addTo(map);
    /***  END MARKERS  ***/
  ```

  Zoom way out. You should have 3 markers.  
  <p align="center">
    <img src= "Images/6-3markers.JPG"> 
  </p>
  
----------

### III. Add popups to each marker

1. First we need to initialize three variables `var popup1`, `var popup2`, and `var popup3`. Each is paired with a text-string that will be used for the .setHTML() value `var popup1_content` etc. In the past, we have set the content right within `.setHTML()`, but since the content is going to get pretty long, using a variable lets us stay more organized.  
  Copy in this code block:

   ```javascript
    /***  POPUPS  ***/
        
    // Popup for marker 1  
    var popup1_content = '<h2>Play the video to listen to Portland</h2><br>';
        
    var popup1 = new mapboxgl.Popup({ minWidth:'300px' })
        .setHTML(popup1_content);
       
    // Popup for marker 2  
    var popup2_content = '<h2>Press play to listen to London in 1928</h2><br>';
        
    var popup2 = new mapboxgl.Popup({ minWidth:'300px' })
        .setHTML(popup2_content);

    
    // Popup for marker 3  
    var popup3_content = '<h2>Press play to listen to a bison eating</h2><br>';   
        
    var popup3 = new mapboxgl.Popup({ minWidth:'300px' })
        .setHTML(popup3_content);

   /***  END POPUPS  ***/ 
   ```  
   The popups aren't linked to the markers yet. So, we need to edit the markers so that each is linked to one of the popups.
  

2. Find where marker one is initialized and add `.setPopup(popup1)` on a new line between the `.setLngLat` and `.addTo(map)`. It will look like this:
   ```javascript
    // Marker 1 - Portland
    var marker1 = new mapboxgl.Marker({color:'DarkRed'})    
      .setLngLat([-122.6788,45.5212]) // Portland 
      .setPopup(popup1) 
      .addTo(map);
   ```

3. Add `.setPopup(popup2)` to marker2 on a new line between `.setLngLat` and `.addTo(map)`.
4. Add `.setPopup(popup3)` to marker3.
5. Zoom and pan to each marker and check that the popups open.

  <p align="center">
    <img src= "Images/6-3markers-Wpopup.JPG"> 
  </p>

----------

### IV. Embed a YouTube video player in popup 1

To embed a YouTube Video, we can add an iframe to the HTML content of a popup by adding it within the popup's HTML content. To do so, we create a string that contains html into the variable `popup1_content`. To help keep our code organized we can concatenate or "join together" multiple text strings. We will use `+=` to append more html text to the end of the existing variable.  

A quick lesson on string concatenation:
We can concatenate strings with a plus sign:
   ```javascript
   // the long way
   var x = "Hello";
   x = x + " World";
   ```
   x now equals "Hello World".  
    - OR - 
   ```javascript
   // using += as shorthand
   var x = "Hello";
   x += " World";
   ```
 x now equals "Hello World".
 
 Let's try with the popup content:

1. Locate the popup for marker 1 and use += to append the iframe embed code from [https://www.youtube.com/embed/z1AdmS-LqyA](https://www.youtube.com/embed/z1AdmS-LqyA){:target="_blank"}      
   ```javascript
   popup1_content += '<iframe width="300px" src="https://www.youtube.com/embed/z1AdmS-LqyA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>';
   ```

   It should now look like this:
   ```javascript
    // Popup for marker 1  
    var popup1_content = '<h2>Play the video to listen to Portland</h2><br>';
    popup1_content += '<iframe width="300px" src="https://www.youtube.com/embed/z1AdmS-LqyA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>';
   ```
     The Portland popup should now look like this.
     <p align="center">
    <img src= "Images/6-PortlandPopup.JPG"> 
    </p>

2. Let's also add the source and a link by concatenating another string to the popup 1 content: ```popup1_content += 'Source: Ian Lind, <a href="https://www.youtube.com/embed/z1AdmS-LqyA">YouTube</a>';```

	It should now look like this:
      ```javascript
    // Popup for marker 1  
    var popup1_content = '<h2>Play the video to listen to Portland</h2><br>';
    popup1_content += '<iframe width="300px" src="https://www.youtube.com/embed/z1AdmS-LqyA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>';
    popup1_content += 'Source: Ian Lind, <a href="https://www.youtube.com/embed/z1AdmS-LqyA">YouTube</a>';
   ```
    <p align="center">
    <img src= "Images/6-PortlandPopupSource.JPG"> 
    </p>

----------

### V. Embed a Soundcloud player in popup 2


1. To make it easier to see your changes, set the map's initial center to the same location as the London popup.
2. Locate the popup for marker 2 `popup2_content` To get an iframe embed code for a Sound Cloud video from London, go to [https://soundcloud.com/londonstreetnoises/cromwell-1928](https://soundcloud.com/londonstreetnoises/cromwell-1928){:target="_blank"}
3. Click the share button, then `Embed`, then copy the code.
    <p align="center">
    <img src= "Images/6-SoundCloud.JPG"> 
    </p>
    
    It's going to be rather long and look similar to the image below. Take a look at the HTML code and see what HTML tags you can recognize.
    <p align="center">
    <img src= "Images/6-EmbedCode.JPG"> 
    </p>
    
4. Locate the popup for marker 2 and use += to append the iframe embed code to the popup content string.
    <p align="center">
    <img src= "Images/6-SoundCloud.JPG"> 
    </p>

5. Lastly, let's also add the source and a link using an anchor tag ```popup2_content += 'Source: LondonStreetNoises.co.uk, <a href="https://soundcloud.com/londonstreetnoises"> SoundCloud </a>';```


    <p align="center">
    <img src= "Images/6-LondonPopup.JPG"> 
    </p>


----------

### VI. Embed a sound file using an html audio player in popup 3
Now let's add a sound file from a relative location (one that you have stored on your computer).
  
The National Park Service has a whole library of sounds that you can download: [https://www.nps.gov/yell/learn/photosmultimedia/soundlibrary.htm](https://www.nps.gov/yell/learn/photosmultimedia/soundlibrary.htm){:target="_blank"}. "They may be downloaded and used without limitation; however, please credit the 'National Park Service' where appropriate".  

The sound file you downloaded from the R drive is a recording of a bison eating `yell-YELLBisonEating150313.mp3`. Have a listen to it using the default audio player on your computer.

1. To make it easier to see your changes, set the map's initial center to the same location as the Yellowstone popup.
2. Locate the popup for marker 3 `popup3_content` 
3. Append a string containing an [HTML audio tag](https://www.w3schools.com/tags/tag_audio.asp){:target="_blank"}.
    ```javascript
    popup3_content += '<audio controls><source src="PATH_TO_FILE" type="audio/mpeg">Your browser does not support the audio element.</audio>';
    ```
4. Replace the `PATH_TO_FILE` with the path to the file _relative_ to path to this html file. If it's in the sounds folder, it is going to be `sounds/yell-YELLBisonEating150313.mp3`  

   **VERY IMPORTANT NOTE:** The path and file name are not case-sensitive locally, but the Pages server is!! For this to work on the web, make sure your path and file name use the same case for all characters as the src as the folder and file. 
   ```javascript
   It should look like this:
   // Popup for marker 3  
    var popup3_content = '<h2>Press play to listen to a bison eating</h2><br>';   
    popup3_content += '<audio controls><source src="sounds/yell-YELLBisonEating150313.mp3" type="audio/mpeg">Your browser does not support the audio element.</audio>';
    ```
    <p align="center">
    <img src= "Images/6-YellowstonePopup.JPG"> 
    </p>

5. And of course, let's add linked attribution ```popup3_content += 'Source: NPS/Jennifer Jerret, <a href="https://www.nps.gov/yell/learn/photosmultimedia/sounds-bisoneating.htm">NPS</a>';```

    <p align="center">
    <img src= "Images/6-YellowstonePopup.JPG"> 
    </p>



----------

### VII. Add an absolute link to an image to popup3 file
The audio file of the bison eating is great, but it could use a visual. Let's add the image that the NPS used at https://www.nps.gov/yell/learn/photosmultimedia/sounds-bisoneating.htm. We can use an img tag and set the src to the image URL. The steps below will show you how.

1. Visit the site with the bison sounds clip at [https://www.nps.gov/yell/learn/photosmultimedia/sounds-bisoneating.htm](https://www.nps.gov/yell/learn/photosmultimedia/sounds-bisoneating.htm){:target="_blank"}  and right click on the image > copy image link
   <p align="center">
    <img src= "Images/6-CopyImageLink.JPG"> 
    </p>
2. Paste the link into a new tab in browser your browser. TADA! We can use this URL as the absolute path to this image. Don't worry, we'll add the source! 
3. Append an HTML img tag to `popup3_content`
   ```javascript
   popup3_content += '<img class="popupImage" src="PATH_TO_FILE">' ;
   ```
   Note: `<img>` is a self-closing tag, so we don't need a second tag to close it.
4. Replace the `PATH_TO_FILE` with the bison image link `https://www.nps.gov/yell/learn/photosmultimedia/images/ndh-yell-bison-gibbon_2.jpg?maxwidth=1200&maxheight=1200&autorotate=false`
5. Is the image way too big for the popup? Let's use CSS to set its width to 100% of the parent element. We already gave it a class named `popupImage`, so add the following to the `<style>` section in the `<head>`. 
   ```css
   .popupImage{
       width:100%;
    }
   ``` 
 
6. Let's add more attribution. On the next line, add:
   ```javascript
    popup3_content += 'Source: NPS/Neal Herbert, <a href="https://www.nps.gov/yell/learn/photosmultimedia/sounds-bisoneating.htm">NPS</a>';
   ```

 <p align="center">
    <img src= "Images/6-YellowstonePopupWImage.JPG"> 
    </p>


----------

### VIII. Add alt text to the image
To add a little more accessibility to our page, we should add text that screen readers can read adding an alternate or "alt" attribute to our image tag.

1. Review the HTML reference for the `alt` attribute of an `<img>` tag: [https://www.w3schools.com/tags/att_img_alt.asp](https://www.w3schools.com/tags/att_img_alt.asp){:target="_blank"}
2. In the img tag add `alt=" Description of photo"`, and add your own description of the scene. 
   Here is what I wrote:
   
 <p align="center">
    <img src= "Images/6-AltText.JPG"> 
    </p>

----------

### IX. Add buttons to jump to each location

Now let's add some UI to make it easier to get to each location.

1. Near the top of the `<body>` we can add three buttons, where it says "Insert the button elements here". One for each marker:
   ```html
      <button class='fly' id='PortlandButton'>Jump to Portland</button>
      <button class='fly' id='LondonButton'>Jump to London</button>
      <button class='fly' id='YellowstoneButton'>Jump to Yellowstone</button> 
   ```
   These are all styled by the `.fly` class which was already added to the `css` in the `head` for you.
    <p align="center">
    <img src= "Images/6-Buttons.JPG"> 
    </p>
2.  The buttons don't actually do anything until we add JavaScript "click" listeners to each button, and within the scope of the listener, we can use a `map.JumpTo` function to change the map view. Here are the first 2:
   ```javascript
    /***  LISTENERS  ***/
        
    // Add a 'Listener' to the button element with the ID 'LondonButton'.
    document.getElementById('LondonButton').addEventListener('click', function () {
            map.jumpTo({
                center: [-0.1534307, 51.501223], 
                zoom: 11
            });
    });
        
    // Add a 'Listener' to the button element with the ID 'PortlandButton'.
    document.getElementById('PortlandButton').addEventListener('click', function () {
            map.jumpTo({
                center:[-122.6788,45.5212], 
                zoom: 9
            });
    });
        
    /***  END LISTENERS  ***/
   ```
   
3. Add the listener for the button element with the ID 'YellowstoneButton' on your own. Use the same center as the marker and a zoom level of 9.
  
Try all 3 buttons, open all 3 popups, and listen to all 3 recordings. Does everything work? Great. <br>
If not, check that console for errors and follow the thread. Do you use the correct ID for each element and corresponding function? What line number has an error? Do you close all strings using balanced quotation marks? 

----------

<h2 align="center"> Part B. Fonts</h2>


### I. Adding a font to the map

Assume a client has asked you to find a free-to-use "fun or whimsical" font for this map.

1. Visit [https://fonts.google.com/](https://fonts.google.com/){:target="_blank"} choose a "fun or whimsical" font, but make sure it is still legible. 
2. Get the HTML/CSS code by clicking "get font" > "Get embed code"
3. Insert the html into the `<head>` of your site.
   e.g. If I picked Martel, I would insert the following code block. You should pick a different font, and you'll be asked to explain your choice for the assignment submission:
   ```html
      <!--   Link to Google font-->
      <link rel="preconnect" href="https://fonts.gstatic.com">
      <link href="https://fonts.googleapis.com/css2?family=Martel&display=swap" rel="stylesheet">
   ```
4. Set the font for the html `button` elements:
   In the `<style>` section, set it with the font-family that you selected.
   e.g. If I picked Martel, the selector for `button` elements would look like this:
   ```css
   button {
        font-family: 'Martel', serif;
        font-weight: 600;
    }
   ```
   
5. Set the font for the popups:
   In the `<style>` section in the `head`, add in the existing selector for the class `.mapboxgl-popup` and add the font-family that you selected. Adjust the size of the font if yours feels too big, or too small. If I picked Martel, the new class would look like this:
   ```css
      .mapboxgl-popup {
          min-width: 325px;
          /*add the css for the popup font here */
          font-family: 'Martel', serif;
      } 
    ```

Here is an example with Martel. Yours should use a different font.
   <p align="center">
	    <img src= "Images/6-PortlandPopupWFonts.JPG">
   </p>


<p align="center">
      <img src="https://media2.giphy.com/media/lTpme2Po0hkqI/giphy.gif?cid=790b7611e7df5c85dd11452d8b06e0102c02acc014faa891&rid=giphy.gif&ct=g" alt="That's all folks!">
    </p>

----------  

### Extra challenge tasks

1. The hyperlinks for the image sources all open in the same tab as your map. It might be better to open them in a new tab instead. Check out at the [W3Schools target reference](https://www.w3schools.com/tags/att_a_target.asp){:target="_blank"}. Add the target `_blank` to each anchor tag so the links will open in a new tab.
2. Use a different font for the sources. 
3. Add a "next" button somewhere static on the page _or_ to each popup. Set that button to call a function that opens the popup for the next marker and jumps or flies to it. Use the buttons to cycle through all your markers.

