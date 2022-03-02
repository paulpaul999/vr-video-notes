# VR: Fisheye to Equirectangular (VR180)

These are some notes on how to convert stereoscopic (side-by-side, SBS) [virtual reality videos](https://en.wikipedia.org/wiki/360-degree_video) from [fisheye projection](https://en.wikipedia.org/wiki/Fisheye_lens) to [equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection).

**Notes:**

- Fisheye is assumed to have a field of view (FOV) of **200°** in the listed commands. *(Feel free to adjust FOV to fit your material.)*
- This tutorial relies on __ffmpeg's [v360 filter](https://ffmpeg.org/ffmpeg-filters.html#v360)__. Note that there are ffmpeg versions out there that don't include this filter.
- These commands were tested on macOS and Linux (Ubuntu).

## Command

```sh
ffmpeg -i fisheye.mp4 -filter:v "v360=input=fisheye:ih_fov=200:iv_fov=200:output=equirect:in_stereo=sbs:out_stereo=tb,crop=iw*(1/2):ih,stereo3d=tbl:sbsl" -map 0 -c copy -c:v libx265 -crf 18 -pix_fmt yuv420p equirectangular_LR_180.mp4
```

*`ih_fov` and `iv_fov` tune FOV of input fisheye material*

## Understanding the command

To understand the command, let's split it up into its video filter steps.


**Fisheye to equirectangular (over-under / top-bottom):**

```sh
ffmpeg -i fisheye.mp4 -vf v360=input=fisheye:ih_fov=200:iv_fov=200:output=equirect:in_stereo=sbs:out_stereo=tb eq.mp4
```

`out_stereo` parameter is set to top-bottom (`tb`) instead of side-by-side (`sbs`). This is because with side-by-side mode ffmpeg outputs an equirectangular VR video with 360° FOV. The video filter is called *v360* after all :smiley:. Going for top-bottom mode makes it easier to use other ffmpeg filters to crop and rearrange the stereo images.

**Cropping the center half to get VR180 over-under**

```sh
ffmpeg -i fisheye.mp4 -filter:v "crop=iw*(50/100):ih" cropped.mp4
```

As far as I know the [v360 filter](https://ffmpeg.org/ffmpeg-filters.html#v360)

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
