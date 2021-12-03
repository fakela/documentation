---
title: Document inputs
excerpt: ''
next:
  pages:
    - limitations
  description: ''
---
## Documents

**File types**
Our APIs support different types of documents like images (JPG, PNG, WEBP), scanned PDF or native PDF. When using PDF files, a maximum number of pages is enforced depending on the document parsing API used. See [Technical limitations](doc:limitations) for more information.

**Payload formats**
We currently support three different payload formats when sending your document to our APIs:
* a **binary file** via multipart/form-data encoding
* a **base64** encoded document via application/json encoding
* a **public URL** (via HTTPS) where the document is hosted

See [Prediction](doc:prediction) for more information.


## Working with images
 
**Supported filetypes**

We support JPG, PNG and WEBP format. Note that our APIs have a maximum file size limitation, think about downsizing your input images if you manipulate heavy files. Always prefer JPG over PDF for scans and photos (as images are processed faster).


**Tips for images** 
- **Reduce heavy or big images**: downscale your image to have a faster upload time and processing time. Because the text can be very small sometimes, resizing the image too much will make it impossible to read. The rule of thumb is that big images should be resized close to 3 megapixels.
- **Do not upscale**: never upscale a low-resolution image on your side! This will decrease the algorithm accuracy. It is best to avoid very low-resolution images, if possible.
- **Keep the aspect ratio**: never change the original aspect ratio.
- **Do not preprocess images**: it is not necessary to transform your image in black and white or change brightness/contrast if the image looks fine.
- **Ask the chat!**: If you have any questions related to your image input data, feel free to ask the chat to talk to an expert.

## Working with PDFs

Our APIs support multi-page PDF files as well. Because we need to convert the PDF pages to actual images, the processing time may be longer compared to image processing.

**Tips for PDFs** 
>- **Best with digital documents**: PDF documents should be reserved for digital documents only for maximum performance.
>- **Working with several pages**:  your PDF may contain several pages. In this scenario, you will receive both predictions at the page level and at the document level. See [JSON response scheme](doc:prediction#json-response) documentation for more details.
>- **Limitations**: there is a maximum number of pages you can send, check the Documentation page of your selected API.