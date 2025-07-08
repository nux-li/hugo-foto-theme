# Foto, a theme for [Hugo](https://gohugo.io/), the world famous static site generator

The intent of this theme is to provide a gallery solution for photographers wanting to publish their work as a photo gallery. Together with the bundled software Hippo (Hugo Image Preprocessor) images placed in the content folder will be resized, with or without watermark. Metadata is extracted and placed in Hugo content pages.

![screenshot](https://github.com/nux-li/hugo-foto-theme/blob/main/images/hugo-foto-theme.png?raw=true)

[EXAMPLE SITE](https://c3n.es/)

Features

## Prerequisites

This theme uses [Hippo](https://github.com/nux-li/hippo) for extraction of metadata, resizing of images, and for generating front matters for every image and album. 
Hippo is written in Kotlin, and you will need Java Runtime Environment (Java version 21 or newer) on your machine in order to run it.

In order to take full advantage of this theme, you should have a selection of photos with metadata attached. 
For preparing photos one can use software such as 
[Darktable](https://www.darktable.org/), 
[Adobe Lightroom](https://lightroom.adobe.com/), 
[On1 Photo Raw](https://www.on1.com/products/photo-raw/), 
or similar. These programs can be used to add titles and descriptions as metadata for your photos.

The following metadata fields are extracted from each photo:
* title
* description
* credit
* capture date and time
* keywords
* focal length
* aperture / f-number
* exposure time
* iso equivalent
* camera make and model

## Installation
Make sure you have Java version 21 or newer on your machine. https://jdk.java.net/24/

### Add theme as a Git Submodule

```sh
git init
git submodule add --depth=1 https://github.com/nux-li/hugo-foto-theme.git themes/foto
```

Then update your `hugo.toml` with the name of the theme:
```toml
theme = "foto"
```

Also add this to the end of the `hugo.toml` file:
```toml
[params]
    credit = '** Your name **'
```
Replace `** Your name **` with your name.

## Getting started

### Run demo site

In order to test the theme with example photos, do this:

* Go to the theme directory
```sh
cd theme/foto
```
* Use `hippo` to create demo pages
```shell
./hippo.sh --demo
```
* Go to back to your project's root directory 
```sh
cd ../..
```
* Start Hugo
```shell
hugo server -D
```
In order to see your demo site, enter [`localhost:1313`](http://localhost:1313/) in the address bar of your browser.

### Remove demo pages 

In order to delete the demo pages, use the clear flag with `hippo`:
```shell
cd theme/foto
./hippo.sh --clear
```
This operation is a bit destructive, and you should probably not use it once you start using your own images.

### Start using your own photos
Now you can copy your own images into different albums within the `content/albums` directory. 
Is it possible to have several levels of subfolders / sub-albums. Choose how you will group your photos: 
by geography, by style, by date etc.

When you have copied your images to different subfolders within `content/albums`, you can run `hippo` again (but if you want watermarks, please read further):
```shell
cd theme/foto
./hippo.sh 
```

### Use your own watermark with your photos
There is two kinds of watermarks that can be added to your photos. The watermark files should be placed 
under `assets/watermarks`:

| Filename             | Description                                                       |
|----------------------|-------------------------------------------------------------------|
| watermark_main.png   | Visible watermark to be placed in one of the image's four corners |
| watermark_subtle.png | Barely visible watermark placed in the middle of the image  |

 

You can use your own watermarks by preparing two PNGs in the above mentioned location.
By using an extra option when running `hippo`, your watermark will be placed in a corner of every 
image (Certain size requirements apply here). The watermark option requires one of the following placement codes:

| Placement code | Watermark placement        |
|----------------|----------------------------|
| UL             | Upper left corner          |
| UR             | Upper right corner         |
| LL             | Lower left corner          |
| LR             | Lower right corner         |
| UL_C           | Upper left corner + center |
| UR_C           | Upper right corner + center         |
| LL_C           | Lower left corner + center          |
| LR_C           | Lower right corner + center         |

In order to add a watermark in the lower left corner and a barely visible watermark in the middle, add
option `--watermark LL_C` to the `hippo` command:


Example:
```shell
cd theme/foto
./hippo.sh --watermark LL_C
```

Start Hugo from Hugo projects root folder
```shell
hugo server -D
```
And watch your site In order to see your demo site, by entering [`localhost:1313`](http://localhost:1313/) in the address bar of your browser.

Or if you site is ready for production, and you have specified your domain in the baseURL setting, you can generate files for production:

```shell
hugo --environment production --cleanDestinationDir
```

## Contributing

If you find a bug feel free to use the [issue tracker](https://github.com/nux-li/hugo-foto-theme/issues) to let me know. 
