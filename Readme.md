# Awesome ffmpeg

Things that you can make with [ffmpeg](https://ffmpeg.org/) and a bit of command line magic.


### Convert mp4 to mkv format, without recoding

```
ffmpeg -i input.mp4 -vcodec copy -acodec copy output.mkv
```


### Cut video

```
ffmpeg -i a.mp4 -ss 00:00:10 -t 01:32:14 b.mp4
```
The -ss parameter is to cut from the beginning
The -t is for the duration, and is optional


### Concatenate videos

```
ffmpeg -i a.mkv -i b.mkv -i c.mkv -filter_complex concat=n=3:v=1:a=1 full_video.mkv
```
The "n" parameter of the concat is the number of input files to be joined together.

DVD can also be converted with this method by concatenating the VOB files


### Get the audio from a video to mp3 format

```
ffmpeg -i videofile.mp4 -vn -acodec copy audiofile.audio extension
```
The mp4 and mkv formats support multiple audio file formats.
To get information from the internal video and audio formats, use
```
ffmpeg -i videofile.mp4
```


### Convert anything to mp3 format

```
ffmpeg -i a.ext -codec:a libmp3lame -q:a 0 a.mp3
```

The -q:a part defines the quality; the higher the value, the lower the sound quality is:

```
Parameter  -  Bitrate
-q:a 0   ->   220-260
-q:a 1   ->   190-250
-q:a 2   ->   170-210
-q:a 3   ->   150-195
-q:a 4   ->   140-185
-q:a 5   ->   120-150
-q:a 6   ->   100-130
-q:a 7   ->    80-120
-q:a 8   ->    70-105
-q:a 9   ->    45- 85
```

The bitrate can be fixed value (but usually this gives worse size/quality ratio than variable bitrate): -q:a 256k


### Convert avi to mkv

```
ffmpeg -i a.avi -c:v libx264 -crf 19 -preset slow -c:a aac -strict experimental -b:a 256k -ac 2 a.mkv
```

The -b:a sets the audio quality.
The -preset changes the speed and quality of the conversation:
```
ultrafast - worst video quality
superfast
veryfast
faster
fast
medium – default preset
slow
slower
veryslow - best video quality
```


### Add utf8 subtitle to video

```
ffmpeg -i in.mkv -i in.ass -c:v copy -c:a copy -c:s copy -map 0:0 -map 0:1 -map 1:0 -sub_charenc UTF-8 -disposition:s:0 default out.mkv
```

You can convert any subtitle file to .ass file format with this:
```
ffmpeg -i in.srt out.ass
```
