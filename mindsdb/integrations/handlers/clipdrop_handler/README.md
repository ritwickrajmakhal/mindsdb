# Clipdrop Handler

Clipdrop handler for MindsDB provides interfaces to connect to Clipdrop via APIs.

## About Clipdrop

The Clipdrop API allows you to integrate best-in-class AI to your apps in minutes.

## Implemented Features

- [x] Clipdrop ML Handler
  - [x] Remove Text from Image
  - [x] Remove Background from Image
  - [x] Generate Image from sketch
  - [x] Generate Image from text
  - [x] Reimagine the Image
  - [x] Replace Background in Image
  - [x] Upscale Image
  - [x] Product photography
  - [x] Uncrop Image

## Example Usage

The first step is to create a ML Engine with the new `clipdrop` engine.

~~~~sql
CREATE ML_ENGINE clipdrop_engine
FROM clipdrop
USING
  clipdrop_api_key = 'your_api_key';
~~~~


The next step is to create a model with a `task` that signifies what type of transformation or generation is needed. The supported values for `task` are as follows:

- [remove_text](#remove-text-from-image)
- [remove_background](#remove-background-from-image)
- [sketch_to_image](#generate-image-from-sketch)
- [text_to_image](#generate-image-from-text)
- [reimagine](#re-imagine-the-image)
- [replace_background](#replace-background-in-image)
- [upscale](#upscale-image)
- [product_photography](#product-photography)
- [uncrop](#uncrop-image)

## Create a model

### Remove Text from Image

~~~~sql
CREATE MODEL mindsdb.clipdrop_rt
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "remove_text",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_rt
WHERE image_url = "https://onlinejpgtools.com/images/examples-onlinejpgtools/calm-body-of-water-with-quote.jpg";
~~~~

### Remove Background from Image

~~~~sql
CREATE MODEL mindsdb.clipdrop_rb
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "remove_background",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_rb
WHERE image_url = "https://static.clipdrop.co/web/apis/remove-background/input.jpg";
~~~~

### Generate Image from Sketch

~~~~sql
CREATE MODEL mindsdb.clipdrop_s2i
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "sketch_to_image",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_s2i
WHERE image_url = 'https://img.freepik.com/free-vector/hand-drawn-cat-outline-illustration_23-2149266368.jpg'
  AND text = 'brown cat';
~~~~

### Generate Image from Text

~~~~sql
CREATE MODEL mindsdb.clipdrop_t2i
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "text_to_image",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_t2i
WHERE text = 'Imagine a software engineer';
~~~~

### Re-imagine the Image

~~~~sql
CREATE MODEL mindsdb.clipdrop_reimagine
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "reimagine",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_reimagine
WHERE image_url = "https://static.clipdrop.co/web/apis/remove-background/input.jpg";
~~~~

### Replace Background in Image

~~~~sql
CREATE MODEL mindsdb.clipdrop_rbi
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "replace_background",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_rbi
WHERE image_url = "https://static.clipdrop.co/web/apis/remove-background/input.jpg"
  AND text = "Empty road";
~~~~

### Upscale Image

~~~~sql
CREATE MODEL mindsdb.clipdrop_upscale
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "upscale",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_upscale
WHERE image_url = "https://imgv3.fotor.com/images/slider-image/Blurry-low-quality-female-portrait-picture.jpg"
  AND target_width = 800
  AND target_height = 580;
~~~~

### Product Photography

~~~~sql
CREATE MODEL mindsdb.clipdrop_pp
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "product_photography",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_pp
WHERE image_url = "https://www.nilkamalfurniture.com/cdn/shop/files/PARDSRDB_SRB_IVR_600x.jpg"
  AND background_color_choice = "#ffffff"; -- optional
~~~~

### Uncrop Image

~~~~sql
CREATE MODEL mindsdb.clipdrop_uncrop
PREDICT image
USING
  engine = "clipdrop_engine",
  task = "uncrop",
  local_directory_path = "/Users/Sam/Downloads/test";
~~~~

~~~~sql
SELECT *
FROM mindsdb.clipdrop_uncrop
WHERE image_url = "https://plugins-media.makeupar.com/smb/blog/author/2024-03-22/7777c9dc-8acf-4a5a-8580-6f8716f31b20.png"
  AND extend_left = 100 -- optional
  AND extend_right = 100 -- optional
  AND extend_up = 100 -- optional
  AND extend_down = 100 -- optional
  AND seed = 50; -- optional
~~~~

**Note:** The `local_directory_path` is the path where the images will be saved after the transformation. The `image_url` is the URL of the image that needs to be transformed.