```
# Convert to PNG
magick mogrify -format png *.jpg
magick mogrify -format png -resize x1000 *.svg
inkscape -w 1024 -h 1024 input.svg --export-filename output.png

# Resize to uniform height
magick mogrify -resize x300 -quality 100 -path ./resized *.png

# Cut circle
find . -name *.png -exec convert {} -alpha on \( +clone -threshold -1 -negate -fill white -draw "circle 150,150 150,0" \) -compose copy_opacity -composite {} \;
find . -name "*.jpg" -exec sh -c 'convert {} -alpha on \( +clone -threshold -1 -negate -fill white -draw "circle 150,150 150,0" \) -compose copy_opacity -composite ${1%.jpg}.png' sh {} \;

# Drop shadow
convert <file>.jpg \( +clone -background black -shadow 60x5+10+10 \) +swap -background white -layers merge +repage <output>.jpg
```
