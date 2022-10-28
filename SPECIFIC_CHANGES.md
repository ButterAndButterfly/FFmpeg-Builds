# FFmpeg Specific Builds

[BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds) builds **full** versions of FFmpeg that include all dependencies,
thus the size of each asset is somehow too large.     
For example, `ffmpeg-master-latest-win64-lgpl.zip` ≈ 100 MB.   
Here, the aim of this repo is to smallize the asset size by customize the build configuration.  


## Changes compared to [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds)
+ `.github/workflows/*`
    + remove all the `*.yml`  
    + create `release.yml`  

+ `build.sh`
set `FF_CONFIGURE="${FF_SPECIFIC_CONFIGURE:-$FF_CONFIGURE}"` before the command
```
./configure --prefix=/ffbuild/prefix --pkg-config-flags="--static" \$FFBUILD_TARGET_FLAGS $FF_CONFIGURE \
...
```

+ `util/vars.sh`  
```
- REPO="${GITHUB_REPOSITORY:-btbn/ffmpeg-builds}"
+ REPO="btbn/ffmpeg-builds"
```

## HOW TO BUILD
Follow the steps below.

+ Set up Github Action secret/env `FF_SPECIFIC_CONFIGURE`  
Here is an example.  
```
--disable-debug --disable-doc --disable-ffplay --disable-ffprobe --enable-static --disable-shared --disable-network --disable-autodetect --disable-decoders --disable-gpl --disable-version3 --enable-decoder='h264,aac*,mp3*,mp4' --disable-encoders --disable-demuxers --enable-demuxer='concat,mov,m4v,flv,mp3' --disable-muxers --enable-muxer='flv,mp4,mp3' --enable-encoder='libmp3lame,mp3' --disable-parsers --enable-parser=h264 --disable-protocols --enable-protocol='concat,file' --disable-bsfs --enable-bsf='h264_metadata,h264_mp4toannexb' --disable-filters --enable-filter='concat,aresample' --disable-iconv --enable-small
```

In addition, you should trigger the variant `lgpl` to `gpl` or so on in `.github/workflows/release.yml` if needed.  
```
matrix:
    target: [win64, linux64, linuxarm64]
    variant: [lgpl]
```
+ Trigger workflow dispatch manually in Github Actions.

