# Webcam Fun

#Objective
In this exercise, I made a photobooth with javaScript. There is a 'Take Photo' button to call the takePhoto() function on click event. Input elements to change the RGB on the screen. The video is being piped into a canvas element. Once the canvas element has the video then you can start taking photos and even download them.

We use the MediaDevices getUserMedia() method to request video and camera access.  

##querySelector
``const video = document.querySelector('.player');
const canvas = document.querySelector('.photo');
const ctx = canvas.getContext('2d');
const strip = document.querySelector('.strip');
const snap = document.querySelector('.snap');``

##Get Video
Get video function

``function getVideo() {
  navigator.mediaDevices.getUserMedia({ video: true, audio: false })
    .then(localMediaStream => {
      console.log(localMediaStream);
      video.src = window.URL.createObjectURL(localMediaStream);
      video.play();
    })
    .catch(err => {
      console.error(`OH NO!!!`, err);
    });
}``

##Paint to Canvas
A frame from video and paint it to the cavas on the page

``` function paintToCanvas() {
  const width = video.videoWidth;
  const height = video.videoHeight;
  canvas.width = width;
  canvas.height = height;

 return setInterval(() => {
    ctx.drawImage(video, 0, 0, width, height);
    let pixels = ctx.getImageData(0, 0, width, height);

    pixels = redEffect(pixels);

    pixels = rgbSplit(pixels);
    ctx.globalAlpha = 0.8;

    pixels = greenScreen(pixels);
 
    ctx.putImageData(pixels, 0, 0);
  }, 16);
}
```


