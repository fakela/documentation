---
title: Document inputs
excerpt: ''
next:
  pages:
    - limitations
  description: ''
---
## Documents in Mindee
Documents used in Mindee include semi-structured files such as an invoice, receipt, ID document, W9-forms, train-ticket etc.

## File Types
Our APIs support different types of documents in different format ranging from images (JPG, PNG, WEBP) to scanned PDF or native PDF. When using PDF files or images, a maximum number of pages and file size is enforced depending on the document parsing API used. See [Technical limitations](https://developers.mindee.com/docs/limitations) for more information.

## Payload Formats
We currently support three different payload formats when sending your document to our APIs:
- a **binary file**: via `multipart/form-data` encoding
- a **base64**: encoded document via `application/json` encoding
- a **public URL**: via `HTTPS` 

See [Prediction](https://developers.mindee.com/docs/prediction#payload) for more information.

## Working with Images
When it comes to images, our APIs have a quicker upload and processing time. If you are dealing with large and heavy images, downscale your input images for faster processing.

### Supported Filetypes
We currently support JPG, PNG and WEBP format. 
> 📘 Info
>
> Always choose JPG over PDF for scans and photos (as images are processed faster).

### Tips for Working With Images
- **Reduce heavy or big images**: Downscale your image to have a faster upload time and processing time. However, resizing the image too much will make it impossible to read, as the text will get very small. The rule of thumb is that big images should be resized close to 3 megapixels.
- **Do not upscale**: Never upscale a low-resolution image on your side! This will decrease the algorithm accuracy. It is best to avoid very low-resolution images, if possible.
- **Keep the aspect ratio**: Never change the original aspect ratio.
- **Do not preprocess images**: It is not necessary to transform your image in black and white or change brightness/contrast if the image looks fine.
- **Limitations**: There is a maximum number of images you can send, check the [Documentation page](https://developers.mindee.com/docs/platform-tour#api---documentation) of your selected API and see [Technical limitations](https://developers.mindee.com/docs/limitations) for more information.
- **Ask the support**: If you have any questions related to your image input data, feel free to use the chat to talk to an expert or ask your question in our [slack community](https://slack.mindee.com/)


## Working with PDFs
Our APIs support multi-page PDF files. However, the processing time may be longer compared to image processing, because we need to convert the PDF to image first.

### Tips for Working With PDFs
- **Best with digital documents**: PDF documents should be in form of digital documents for maximum performance.
- **Working with several pages**:  Your PDF may contain several pages. In this scenario, you will receive both predictions at the page level and at the document level. See [JSON response scheme](https://developers.mindee.com/docs/prediction#json-responsep) documentation for more details.
- **Limitations**: There is a maximum number of pages you can send, check the [Documentation page](https://developers.mindee.com/docs/platform-tour#api---documentation) of your selected API and see [Technical limitations](https://developers.mindee.com/docs/limitations) for more information.
