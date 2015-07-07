# How Recompile FFMPEG Enabling X264 Support #

Folloeing the instruction to checkout the code and recompile it.

```
git clone http://github.com/FFmpeg/FFmpeg.git
cd FFmpeg
git checkout n0.7.2

./configure --enable-gpl --enable-version3 --enable-nonfree --enable-postproc --enable-pthreads --enable-libfaac --enable-libmp3lame --enable-libtheora --enable-libx264 --enable-libxvid --enable-libx264 --disable-yasm


make
sudo make install
```




# x264 Transcoding Settigs #

Following you can find some tricky command line to transcode avi file in h264 wrapped in a transport stream container using a constant bitrate and at high quality. The presets mentioned in the examples can be downloaded form the following link:


http://test-code-hosting-manuele.googlecode.com/files/presets-x264.tgz

```
# 1080p
../../FFmpeg/ffmpeg -i ED_HD.avi  -r 24 -pass 1 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-fastfirstpass.ffpreset -keyint_min 240  -b 7000k -minrate 7000k -maxrate 7000k  -bufsize 1835k -threads 0 ED_1080p-pass1.ts

../../FFmpeg/ffmpeg -i ED_HD.avi  -r 24 -pass 2 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-hq.ffpreset -keyint_min 240  -b 7000k -minrate 7000k -maxrate 7000k  -bufsize 1835k -threads 0 ED_1080p.ts

# 720p
../../FFmpeg/ffmpeg -i ED_HD.avi -s 1280x720 -aspect 16:9 -r 24 -pass 1 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-fastfirstpass.ffpreset -keyint_min 240  -b 5000k -minrate 5000k -maxrate 5000k  -bufsize 1835k -threads 0 ED_720p-pass1.ts

../../FFmpeg/ffmpeg -i ED_HD.avi -s 1280x720 -aspect 16:9 -r 24 -pass 2 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-hq.ffpreset -keyint_min 240  -b 5000k -minrate 5000k -maxrate 5000k  -bufsize 1835k -threads 0 ED_720p.ts

# 480p
../../FFmpeg/ffmpeg -i ED_HD.avi -s 704x480 -aspect 16:9 -r 24 -pass 1 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-fastfirstpass.ffpreset -keyint_min 240  -b 3000k -minrate 3000k -maxrate 3000k  -bufsize 1835k -threads 0 ED_480p-pass1.ts

../../FFmpeg/ffmpeg -i ED_HD.avi -s 704x480 -aspect 16:9 -r 24 -pass 2 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-hq.ffpreset -keyint_min 240  -b 3000k -minrate 3000k -maxrate 3000k  -bufsize 1835k -threads 0 ED_480p.ts

# 360p
../../FFmpeg/ffmpeg -i ED_HD.avi -s 640x360 -aspect 16:9 -r 24 -pass 1 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-fastfirstpass.ffpreset -keyint_min 240  -b 1500k -minrate 1500k -maxrate 1500k  -bufsize 1240k -threads 0 ED_480p-pass1.ts

../../FFmpeg/ffmpeg -i ED_HD.avi -s 640x360 -aspect 16:9 -r 24 -pass 2 -f mpegts -an -vcodec libx264 -fpre ~/Downloads/segmenter/script/presets/libx264-hq.ffpreset -keyint_min 240  -b 1500k -minrate 1500k -maxrate 1500k  -bufsize 1240k -threads 0 ED_480p.ts
```