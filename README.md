Simple single-file JavaScript library to break a video down into individual frames.

 * Currently only supports mp4 files.
 * Check browser support: https://caniuse.com/webcodecs
 * All credit for this code goes to authors of [official WebCodecs demos](https://w3c.github.io/webcodecs/samples/video-decode-display/) and of [mp4box.js](https://github.com/gpac/mp4box.js/).

### Usage
```js
import getVideoFrames from "https://deno.land/x/getVideoFrames@v0.0.1"

// `getVideoFrames` expects a video URL.
// If you have a file/blob instead of a videoUrl, turn it into a URL like this:
let videoUrl = URL.createObjectURL(fileOrBlob);

for await (let frame of getVideoFrames(videoUrl)) {
  // `frame` is a VideoFrame object
  ctx.drawImage(frame, 0, 0, canvas.width, canvas.height);
  frame.close();
}

URL.revokeObjectURL(fileOrBlob); // revoke URL to prevent memory leak
```
