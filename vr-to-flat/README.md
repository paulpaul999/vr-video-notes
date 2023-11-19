# VR: How to Convert VR Videos to 2d/Flat Videos

*Note: You need a version of __ffmpeg__ that has the __[v360](https://ffmpeg.org/ffmpeg-filters.html#v360)__ filter.*

You can tune the following parameters:
- `d_fov`: In simple terms: Zooms in or out.
- `pitch`: Angle to tilt the "virtual camera" towards the top/bottom. 
- `w`, `h`:  Width & Height of the output video.

## VR180 / Equirectangular

```
ffmpeg -i equirectangular.mp4 -filter:v "v360=input=hequirect:output=flat:in_stereo=sbs:out_stereo=2d:d_fov=125:w=1920:h=1080:pitch=-30" -map 0 -c copy -c:v libx265 -crf 18 -pix_fmt yuv420p flat.mp4
```

## Fisheye

```
ffmpeg -i fisheye.mp4 -filter:v "v360=input=fisheye:ih_fov=200:iv_fov=200:output=flat:in_stereo=sbs:out_stereo=2d:d_fov=125:w=1920:h=1080:pitch=-30" -map 0 -c copy -c:v libx265 -crf 18 -pix_fmt yuv420p flat.mp4
```

*Note: `ih_fov` and `iv_fov` tune FOV of input fisheye material. (200° in this example)*
