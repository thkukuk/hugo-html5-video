# hugo-html5-video

This is a html5 video theme for [Hugo](https://gohugo.io/) providing a shortcode `video` using the [HTML5 video element](https://www.w3schools.com/html/html5_video.asp).

## Demo

* Real-life example at https://www.thkukuk.de/Modellbahn/Galerie/Weihnachtszug/

## Features

This `{{< video src="<name>" >}}` shortcode will include the video with the name `name` and a supported extension from a [page bundle](https://gohugo.io/content-management/page-bundles/) in the page and generates [structured data](https://schema.org/VideoObject) for it.

Since different browsers support a different set of video formats, this shortcode does not filter videos according their format ir extension. The section [HTML Video Formats](https://www.w3schools.com/html/html5_video.asp) contains a table, which video formats are supported by which browser.

## Usage

An example directory/file layout could be:
```
content/
└── post/
    ├── _index.md
    └── hugo-html5-video/       <-- page bundle
        ├── index.md
        ├── video1.mp4          <-- video in mp4 format
        ├── video1.wbem         <-- video in wbem format
        ├── video1.png          <-- thumbnail of video in png format
        └── videos/
            ├── video2.mp4      <-- second video in mp4 format
            ├── video2.jpg      <-- thumbnail of second video in jpg format
            └── video2.meta     <-- sidecar file for second video
```
An example usage of this shortcode to include video2 could be:
```
{{< video src="video2" autoplay="true" muted="true" >}}
```

The `src` argument is mandatory and should contain the name of the video
without extension. In the above example, this could be `src="video1"` or
`src="video2"`.
Additional options to control the appearance are:
- `controls="false"` will disable webbroswer's controls, they are by default enabled.
- `width="xx"`, default is `width="100%"`.
- `height="yy"` defines the video height, by default this is not set.
- `autoplay="true"` will enable autoplay if supported by the browser.
- `loop="true"` will enable playing the video in an endless loop.
- `muted="true"` will switch off sound.
- `preload="auto|metadata|none"` specifies if and how video should be loaded when the page loads.
- `playsinline`

## Structured data

The shortcode creates a `ld+json` script struct of the type `VideoObject`. The content for this is mostly taken from the `*.meta` file, which contains a json struct.

An example content:
```
{
  "Title": "Title of the video",
  "Description": "Description of the video",
  "Duration": "PT89M54S",
  "DateUploaded": "2023-12-24"
}
```
