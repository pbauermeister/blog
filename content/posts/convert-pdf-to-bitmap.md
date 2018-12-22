---
title: "Convert Pdf to Bitmap"
date: 2018-12-22T17:49:31+01:00
draft: false
---

## Converting a PDF file to bitmaps

This command will convert the file `test.pdf` to multiple bitmaps, one per
page, named `test-0.jpg` and so on:
```
convert -density 600 test.pdf -resize 100% -quality 96 test.jpg
```

Adjust the density, size and quality as desired.

## Memory issues

The above command may yield an error such as:
```
convert-im6.q16: DistributedPixelCache '127.0.0.1' @ error/distribute-cache.c/ConnectPixelCacheServer/244.
convert-im6.q16: cache resources exhausted `/tmp/magick-30852s1Yagw7cgAXZ1' @ error/cache.c/OpenPixelCache/3984.
convert-im6.q16: no images defined `test.jpg' @ error/convert.c/ConvertImageCommand/3258.
```

In this case, increase the memory:
```
sudo emacs /etc/ImageMagick-6/policy.xml
```

and edit the sizes like:
```
  <policy domain="resource" name="memory" value="2GiB"/>
```

Do the same for policies with these names: `map`, `area` and `disk`.
