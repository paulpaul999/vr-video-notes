# VR: Fisheye to Equirectangular (VR180)

These are some notes on how to convert stereoscopic (side-by-side, SBS) [virtual reality videos](https://en.wikipedia.org/wiki/360-degree_video) from [fisheye projection](https://en.wikipedia.org/wiki/Fisheye_lens) to [equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection).

**Notes:**

- Fisheye is assumed to have an FOV (field of view) of **200°** in the following command. *(Feel free to adjust parameters according to your material.)*
- This tutorial relies on __ffmpeg__'s __[v360](https://ffmpeg.org/ffmpeg-filters.html#v360)__ filter. Note that there are ffmpeg versions out there that don't include this filter.

## Command

```sh
ffmpeg -i fisheye.mp4 -filter:v "v360=input=fisheye:ih_fov=200:iv_fov=200:output=hequirect:in_stereo=sbs:out_stereo=sbs" -map 0 -c copy -c:v libx265 -crf 18 -pix_fmt yuv420p equirectangular_LR_180.mp4
```

That's it! :boom:

*Note: `ih_fov` and `iv_fov` tune FOV of input fisheye material*

## Note

*(In a past version of this document, some filter steps were explained here. Since the newer version has a much simpler ffmpeg command, those explanations were discarded.)*

## Room for improvement (contributions are welcome)

**Preserve image quality:** When I tested the above-mentioned command the the result came with a slight loss in image sharpness. Here are some ideas that could improve quality:

- Output Codec (H.265):
    - Increase bitrate.
    - Try different encoding [profiles](https://x265.readthedocs.io/en/master/cli.html#profile-level-tier) and/or tune [other parameters](https://x265.readthedocs.io/en/master/cli.html).
- Test different interpolation methods of the `v360` filter. See `interp` parameter.
- Oversampling strategy: E.g. adding additional filters to the chain in order to upscale video before `v360` filter and downscale back afterwards. 


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
