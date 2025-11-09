---
layout: "../../layouts/ProductPage.astro"
title: "Tutorial Product"
price: "$999.00"
image:
    src: "https://bulma.io/assets/images/placeholders/1280x960.png"
    alt: "Placeholder Asset"
category: "Other"
---
## How to Edit Product Information
Everything inside the dashed lines contains the "properties" of the product.
These will be used to automatically generate the product cards, as well as some elements on the product pages.

Just replace their values with what you want to replace them with!

* `layout`: Do not change this value.
* `title`: The title of the product.
* `price`: The price of the product. Format as "$XXX.XX".
* `image`: The image that appears on the product card and on the left side of the product page. It has two parts:
    * `src`: Where the image is stored. Place the image in the `src/assets` folder, and change the file name of `src` to the filename of that image.
    * `alt`: If the image cannot load, or if the viewer is using a screen reader, this text will be shown instead. Just describe what is in the image
* `category`: This can be whatever you want. Products with the same category will (eventually) be group together in their own category pages. For example, every product of the category `Tumbler` will be included in the Tumbler page.

## How to Edit Product Description
Everything else in this file, below the dashed section, is the description of the product. It uses [Markdown formatting](https://www.markdownguide.org/), which you can learn about at that link. Basically it's just text with some extra features, like **text** *formatting*, links, lists, headers, etc.