# Website-Image-and-audio-downloader

echo "Enter the URL: "
read URL

echo "$URL" > webpage_link.txt

curl -s "$URL" > webpage.html

grep -o -E 'https?://[^"]+\.(jpg|jpeg|png|apng|avif|svg|webp)' webpage.html > images.txt
line=$(wc -l < images.txt)
echo "There are $line images in the link which is provided."

grep -o -E 'https?://[^"]+\.(mp4|mkv|gif|mov|avi|flv)' webpage.html > videos.txt
line_1=$(wc -l < videos.txt)
echo "There are $line_1 videos in the link "

grep -o -E 'https?://[^"]+\.(mp3|ogg|wav)' webpage.html > audios.txt
line_2=$(wc -l < audios.txt)
echo "There are $line_2 audios in the link "

wget -i images.txt
wget -i videos.txt
wget -i audios.txt
