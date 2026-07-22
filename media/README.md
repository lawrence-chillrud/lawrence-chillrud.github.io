# README

How to compress images for viewing on the web:

1. Download ImageMagick

```bash
brew install imagemagick
```

2. Place all photos to be compressed in a directory, then make a directory where you want the compressed versions to be output to

```bash
mkdir <output_dir>
```

3. Run this command:

```bash
mogrify -path <output_dir> -format webp -quality 80 -resize 1280x720\> -auto-orient -strip <input_dir>/*.<file_format>
```

Best options:

`-quality 80` — JPEG quality (1-100; 80 is ideal for web)
`-auto-orient` – Reads the EXIF rotation data from the original JPEG, Physically rotates the image pixels to match that orientation
`-strip` — Removes metadata, EXIF, color profiles (saves 10-15%)
`-format webp` — Convert to WebP format (offers 25-35% better compression than JPEG at the same quality level)
`-resize 1280x720\>` — Resize if larger than 1280x720 (add if needed). The > means "only resize if larger than these dimensions."

Common web widths:

-resize 1920x1080 — Full-width desktop (most common)
-resize 1280x720 — Medium (saves more space)
-resize 800x600 — Thumbnail/mobile-optimized

You can serve WebP to modern browsers and fall back to JPEG for older ones using the <picture> element:

```html
html<picture>
  <source srcset="image.webp" type="image/webp">
  <source srcset="image.avif" type="image/avif">
  <img src="image.jpg" alt="description">
</picture>
```

# Command I used

```bash
mogrify -path stuff_to_sell_web -format webp -quality 80 -auto-orient -strip -resize 1280x720\> stuff_to_sell/*.jpeg
```
