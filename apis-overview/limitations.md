---
title: Technical limitations
excerpt: ''
---
## Request

A set of limits are enforced to ensure the safety of Mindee's parsing document APIs. Among others:
* a maximum file size
* a maximum number of pages for PDF
* a maximum request throughput per second
* a maximum request throughput per minute

Inside Mindee Platform, you can find these limits in the documentation tab of your API.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/56777aa-ratelimits.png",
        "ratelimits.png",
        767,
        330,
        "#fcfcfc"
      ],
      "caption": "\"Rate limits\" part of Mindee's platform documentation tab."
    }
  ]
}
[/block]


If you need to raise those limitations, feel free to ask the support team.

## Payload
#### Accepted document files
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "MIME Type",
    "0-0": "Image JPEG",
    "0-1": "image/jpeg",
    "h-2": "Extensions",
    "0-2": "jpeg, jpg",
    "1-0": "Image Portable Network Graphics",
    "1-1": "image/png",
    "1-2": "png",
    "2-0": "Image WEBP",
    "2-1": "image/webp",
    "2-2": "webp",
    "3-0": "Adobe Portable Document Format",
    "3-1": "application/pdf",
    "3-2": "pdf"
  },
  "cols": 3,
  "rows": 4
}
[/block]
Will be supported soon:
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "MIME Type",
    "h-2": "Extensions",
    "0-0": "High Efficiency Image File Format",
    "0-2": "heic, heif",
    "0-1": "image/heif",
    "1-0": "Tagged Image File Format",
    "1-1": "image/tiff",
    "1-2": "tiff, tif"
  },
  "cols": 3,
  "rows": 2
}
[/block]