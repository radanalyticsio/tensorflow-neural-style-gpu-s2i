# Neural-Style S2I

## About

Neural Style, as outlined by Gatys, Ecker and Bethge in _[A Neural Algorithm of Artistic Style, 2015](https://arxiv.org/pdf/1508.06576v2.pdf)_, is a method of training convultional neural nets to produce images that can stylistically mimic paintings. Specifically, a **content** image is painted in the style of **style** image, so for example, you can take your favorite selfie (the content image) and paint it in the style of Van Gogh's Starry Night (the style image). For some great examples, check out [this document](https://github.com/lengstrom/fast-style-transfer/blob/master/README.md) by Logan Engstrom.  

This implementation is based off of a neural-style implementation by [Anish Athalye](https://github.com/anishathalye/neural-style), with some minor edits to his code. More on that [here](https://github.com/RobGeada/neural-style).

## Options
* `STYLE_URL`: The URL at which your desired **style** image lives.
* `CONTENT_URL`: The URL at which your desired **content** image lives.
* `MODEL_URL`: If you already have a `.ckpt` file from a previous run of neural-style, you can point to it here.
* `WIDTH`: The width of your output image. Height is automatically adjusted to maintain aspect ratio. 
* `ITERATIONS`: The number of iterations to train over.

Larger values of `WIDTH` and `ITERATIONS` will increase the quality of the output image at the expense of greater training time.

## Usage
```
oc create template -f https://raw.githubusercontent.com/RobGeada/neural-style-s2i/master/template.json
```
To train with default image settings (style=[Great Wave off Kanagawa](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Tsunami_by_hokusai_19th_century.jpg/1200px-Tsunami_by_hokusai_19th_century.jpg), content=[Chicago Skyline](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Chicago_from_North_Avenue_Beach_June_2015_panorama_2.jpg/800px-Chicago_from_North_Avenue_Beach_June_2015_panorama_2.jpg), width=1000, iterations=1000):
```
oc new-app --template neural-style
```
To train with custom images:
```
oc new-app --template neural-style --param=STYLE_URL=[url of style image] --param=CONTENT_URL=[url of content image] --param=WIDTH=1000 --param=ITERATIONS=1000
```

To evaluate a pre-trained model:
```
oc new-app --template neural-style --param=STYLE_URL=[url of style image] --param=CONTENT_URL=[url of content image] --param=MODEL_URL=[url of model] --param=WIDTH=1000 --param=ITERATIONS=1000
```

## Using Pre-Trained Models
Due to how this implementation of neural-style works, pre-trained models will only work when provided with the _exact same pair of content and style images_. 

## License
The original neural-style code upon which this is based is copyright, the details of which have been provided below.

Copyright (c) 2015-2017 Anish Athalye. Released under GPLv3. See
[LICENSE.txt](https://github.com/RobGeada/neural-style/blob/master/LICENSE.txt) for details.
