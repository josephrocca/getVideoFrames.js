Simple single-file JavaScript library to break a video down into individual frames using the new WebCodecs API.

 * Currently only supports mp4 files.
 * Check browser support: https://caniuse.com/webcodecs
 * All credit for this code goes to authors of [official WebCodecs demos](https://w3c.github.io/webcodecs/samples/video-decode-display/) and of [mp4box.js](https://github.com/gpac/mp4box.js/).

### Usage
```js
<canvas id="canvasEl"></canvas>
<script type="module">
  import getVideoFrames from "https://deno.land/x/get_video_frames@v0.0.4/mod.js"

  let ctx = canvasEl.getContext("2d");

  // `getVideoFrames` requires a video URL as input.
  // If you have a file/blob instead of a videoUrl, turn it into a URL like this:
  let videoUrl = URL.createObjectURL(fileOrBlob);

  await getVideoFrames({
    videoUrl,
    onFrame(frame) {  // `frame` is a VideoFrame object: https://developer.mozilla.org/en-US/docs/Web/API/VideoFrame
      ctx.drawImage(frame, 0, 0, canvasEl.width, canvasEl.height);
      frame.close();
    },
    onConfig(config) {
      canvasEl.width = config.codedWidth;
      canvasEl.height = config.codedHeight;
    },
  });
  
  URL.revokeObjectURL(fileOrBlob); // revoke URL to prevent memory leak
</script>
```

Demo: https://jsbin.com/rokuzabeqi/edit?html,output
