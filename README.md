heroku-buildpack-imagemagick-webp
=================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for vendoring the ImageMagick binaries (with WEBP support) into your project.

## How it works
Rather than pulling down binary dependencies from a package manager and extracting them into place, this buildpack compiles Imagemagick from source the first time an app is built with it. The compiled binaries are cached for future builds, so this penalty is only incurred once.

This has the downside of a (potentially very long) deploy time for the first push, with the benefit of a less-fragile build product that's somewhat less likely to break due to platform and dependency shifts. Or at least, that's the hope!

## Note on Heroku config

Optionally, set the ImageMagick and libwebp versions in a Heroku config like this:

```
heroku config:set IMAGE_MAGICK_VERSION=7.0.5-0
heroku config:set LIBWEBP_VERSION=1.0.3
```

Make sure the versions you're referencing exist in the [ImageMagick releases](http://www.imagemagick.org/download/releases/) and [webp releases](http://downloads.webmproject.org/releases/webp/index.html).

## Verify Installation & Version

You can verify the correct version of ImageMagick by running the following:

```
heroku run "identify --version" -a appname
```

You can verify that ImageMagick was built with libwebp support by running the following:

```
heroku run "identify -list format" -a appname
```

If the output includes ```WEBP* rw-   WebP Image Format (libwebp 0.4.2)``` then you're all set.

## LICENSE - "MIT License"

Copyright (c) 2014 Nick Jensen, https://nrj.io
Copyright (C) 2012 Heroku, Inc.

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.
