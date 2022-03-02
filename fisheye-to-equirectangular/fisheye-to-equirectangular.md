# VR: Fisheye to Equirectangular (VR180)

These are some notes on how to convert stereoscopic (side-by-side, SBS) [virtual reality videos](https://en.wikipedia.org/wiki/360-degree_video) from [fisheye projection](https://en.wikipedia.org/wiki/Fisheye_lens) to [equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection).

**Notes:**

- Fisheye is assumed to have a field of view (FOV) of **200°** in the listed commands. *(Feel free to adjust FOV to fit your material.)*
- This tutorial relies on __ffmpeg's [v360 filter](https://ffmpeg.org/ffmpeg-filters.html#v360)__. Note that there are ffmpeg versions out there that don't include this filter.
- These commands were tested on macOS and Linux (Ubuntu).


## Helpful Links

- https://ffmpeg.org/ffmpeg-filters.html#v360
- https://stackoverflow.com/questions/68114739/unable-to-convert-dual-fisheye-image-to-equirectangular-image-using-ffmpeg-packa
- [FFmpeg Cheat Sheet for 360º video](https://gist.github.com/nickkraakman/e351f3c917ab1991b7c9339e10578049)
- https://github.com/jumpjack/fishconLC
- https://www.reddit.com/r/GearVR/comments/2pydr4/howto_format_180degree_3d_sbs_videos_to_display/
- http://echeng.com/articles/encoding-for-oculus-media-studio/
- https://stackoverflow.com/questions/39685629/re-encode-video-stream-only-with-ffmpeg-and-with-all-audio-streams
- https://stackoverflow.com/questions/12938581/ffmpeg-mux-video-and-audio-from-another-video-mapping-issue/12943003#12943003
- https://creator.oculus.com/blog/encoding-high-resolution-360-and-180-video-for-oculus-go/
