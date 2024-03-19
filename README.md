# Website-Image-and-audio-downloader

#!/bin/bash

echo "Enter the URL: "
read URL

echo "$URL" > webpage_link.txt

curl -s "$URL" > webpage.html

grep -o -E 'https?://[^"]+\.(jpg|jpeg|png|apng|avif|svg|webp)' webpage.html > images.txt
image_count=$(wc -l < images.txt)
echo "There are $image_count images in the link which is provided."

grep -o -E 'https?://[^"]+\.(mp4|mkv|gif|mov|avi|flv)' webpage.html > videos.txt
video_count=$(wc -l < videos.txt)
echo "There are $video_count videos in the link."

grep -o -E 'https?://[^"]+\.(mp3|ogg|wav)' webpage.html > audios.txt
audio_count=$(wc -l < audios.txt)
echo "There are $audio_count audios in the link."

wget -i images.txt
wget -i videos.txt
wget -i audios.txt
