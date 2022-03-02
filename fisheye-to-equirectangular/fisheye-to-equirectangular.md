# VR: Fisheye to Equirectangular (VR180)

These are some notes on how to convert stereoscopic (side-by-side, SBS) [virtual reality videos](https://en.wikipedia.org/wiki/360-degree_video) from [fisheye projection](https://en.wikipedia.org/wiki/Fisheye_lens) to [equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection).

**Notes:**

- Fisheye is assumed to have a field of view (FOV) of **200°** in the listed commands. *(Feel free to adjust FOV to fit your material.)*
- This tutorial relies on __ffmpeg's [v360 filter](https://ffmpeg.org/ffmpeg-filters.html#v360)__. Note that there are ffmpeg versions out there that don't include this filter.
- These commands were tested on macOS and Linux (Ubuntu).
