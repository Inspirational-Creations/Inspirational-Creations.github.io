# About This Repo

This is a catalogue website for my mom and aunt's business, [Inspirational Creations](https://inspirationalcreations.net). They wanted a website that could show all of the products they have for sale. I created a system using [Astro](https://astro.build) where Markdown files describing the products are automatically turned into product pages.

# How to Change the Site

The following is a guide intended for non-technical users about how to add and edit content on this website.

## Using Github and VSCode

Editing this website requires using two pieces of software: [GitHub](https://github.com) and [Visual Studio Code]([https://vscode.dev](https://code.visualstudio.com/)) (or VSCode for short). 
GitHub keeps track of all the changes that are made to the site. 
It keeps a record of everything you change, and it lets you easily download other's changes and upload your changes.
VSCode is a bit like a text editor, but it has some extra features that make editing the pages easier.
I would reccomend adding [this](https://files.catbox.moe/f2ru90.json) to your settings.json file to hide anything you don't need to edit. Press ctrl + shift + p in VSCode, then search for "Preferences: Open User Settings (JSON). Then add that to the file and save. This will hide all of the code files so you can focus on only the content.

## General Workflow

The process of making changes generally goes like this:
* Open the GitHub Desktop app, and press "pull origin" on the top bar. If any changes were made since the last time you edited the site, this will download them for you.
    * If the button says "fetch origin", press it and it should turn into a pull origin button after its done.
* Then, press the "Open in Visual Studio Code" button in the main panel. This will open the website's folder in VSCode.
* Make your changes in VSCode.
* Once you are done, go back to the GitHub Desktop app. On the left side should be a list of all the files you changes and what you changed about them. Write a short summary of what you did, then press the "Commit XX files to **main**" button.
* Once you do that, go to the top to where the pull origin button was, and press "push origin". This will upload the changes to the server host and they should be live on the [inspiratoinalcreations.net](https://inspirationalcreations.net) in about a minute.
    * Like before, if the button says "fetch origin", press it and it should turn into a push origin button after its done.

## Project Structure
For the purposes of what you're doing, there are only three different folders you need to look at. (Everything else should be hidden). 

* The `src/pages` folder has files that define entire pages (such as the about page, or product pages).
* The `src/content` folder has elements that are parts of pages, but not pages themselves (like the alert).
* The `public/assets` folder holds any images you want to reference.

## File Structure
Any files you need to edit should be in the `.md` file format. 
This is similar to a normal text file, but it has some additional formatting options (which are explained later).

At the top of most of these files is an area known as the "frontmatter". 
It contains information about the file which is used by the program in other places.
Every property value should be in "quotation marks" unless I say otherwise.
These values can also be listed in any order.

Everything after the "frontmatter" is the body of the file.

The general format looks like this:
```
---
Everything inside these dashed lines is the frontmatter
---
Everything after them is the body of the file
```
Each thing you can edit has different rules for what is supposed to go in the frontmatter, but the body generally contains the text for that item.

## Editing Content
Some common tasks will be explained below.

### Adding products
Each product is defined as its own `.md` file. These are used to automatically create both the pages for the products, and the product cards that show up on the home page. To add a new product, make a new file in `src/pages/products`. Call the file whatever you want, but make sure it ends in `.md`. The name of the file specifies the URL it is at (for example, calling the file `filename.md` means the product will be at `inspirationalcreations.net/products/filename). The products are also sorted alphabetically by this file name, so you could use that to set a custom order.

#### Frontmatter
* `layout`: This is an internal value so the program knows what the final result should look like. **Make sure this is always set to "../../layouts/ProductPage.astro".**
* `title`: The title of the product
* `price`: The displayed price of the product. Put it in with a dollar sign and cent values for consistency.
* `image`: This is the image that is displayed next to the product. (Currently, only one image is supported). This property has two *sub-properties*:
    * `src`: This is how the program knows what image to use. If you simply put a file name (such as "product.jpg"), it will pull the file of that name from the `public/product-imgs/` folder. If you give it a link to an image (such as https://example.com/product.jpg), it will get the image from that URL. Also, note that you can use any sized image you want, but it will be cropped to square in the product card. The full image *will* be shown on the product page.
    * `alt`: If the image cannot be displayed, this text will be displayed instead. It should describe what is in the image. This is useful in case the image can't load, or if a blind person who can't see the images uses the site.
* `category`: Make this whatever you want. All products that have the same value for `category` will be automatically grouped together in a category page (so people can look at just tumblers, for example).

#### Body
Everything after the frontmatter is the product description. This will only appear in the product's page, and not the card.

#### Example
```
---
layout: "../../layouts/ProductPage.astro"
title: "Example Product"
price: "$999.00"
image:
    src: "tumbler.jpg"
    alt: "A metal tumbler. It has a pink-to-blue gradient."
category: "Other"
---
Product description here
```
---
### Editing the Alert
The **alert** is a banner that appears on top of all pages on the website.

You can edit the alert by changing the `src/content/alert.md` file.

#### Frontmatter
* `visible`: If this is *true*, the alert will be displayed above every page on the site. If it is *false*, it will not. Make sure there are no quotes around this.
* `hue`: This is what color the alert is, in case you want to have different colors for different occasions. The color options are "red", "yellow", "green", "blue", and "purple".
* `brightness`: This is what "shade" of color is used. There are three options: "light", "dark", and "normal".

#### Body
Everything after the frontmatter is the content that is displayed in the alert. 

#### Example
```
---
visible: true

hue: "red"
brightness: "dark"
---
Text goes here
```
---
### Editing the Hero
The **hero** is the larger banner that appears at the top of the home page.

#### Frontmatter
* `size`: How much space the hero takes up. The options are "small" (default), "medium", or "large".
* `title`: The title displayed in the hero
* `subtitle`: The subtitle displayed in the hero

#### Body
Everything after the frontmatter will be shown below the title and subtitle inside the hero.

#### Example
```
---
size: "small"
title: "Inspirational Creations"
subtitle: "Hand-crafted products"
---
Additional content here (if needed)
```
---
### Content Pages
Content pages are any pages which contain things other than products. For example, the "About Us" and "Contact" pages are considered content pages. Any content pages are automatically added to the navigation bar.

#### Adding new Content Pages
Create new content pages as `.md` files in `src/pages`. The name of the files corresponds with its URL (for example, `info.md` will be at `inspirationalcreations.net/info`).

#### Frontmatter
* `layout`: Do not change this value. It should be "/src/layouts/ContentPage.astro" for all content pages.
* `title`: The title of the page. Shown at the top of the page, in the browser tab, and in the navbar
* `image`: The image is defined similarly to product images, with `src` and `alt` sub-properties. If this property is present, it will be shown to the right of the content on desktop or underneath it on mobile. If you do not want there to be an image, remove this property.

#### Content
Anything below the frontmatter will be the content of the page.

#### Example
```
---
title: "About Us"
image:
    src: "https://media.licdn.com/dms/image/v2/C5603AQFEgAsvePUI1A/profile-displayphoto-shrink_200_200/profile-displayphoto-shrink_200_200/0/1516586889315?e=2147483647&v=beta&t=XWiaH_tinCRD38xz9nXIyolFFMF6pg32ucIB0B_NQYk"
    alt: "A picture of Robin and Denise"
layout: "/src/layouts/ContentPage.astro"
---
Inspirational Creations is a...
```

## Markdown Formatting
Below is a list of common markdown formatting options. Everything described here works in the "body" section of all markdown files in this project.

- New Lines: By default, Markdown will put text on two adjacent lines on the same line. If you want to create a new line, place an empty line in between the two lines.
- *Italic text*: Wrap the text you want to be in italics in asterisks, \*like this\*.
- **Bold text**: Wrap the text you want to be bold in two asterisks, \*\*like this\*\*.
    - You can also combine this and do bold and italics by using three sets of asterisks.
- Headings: You can make titles/subtitle by placing a \# before your text, \# like this.
    - The more \#'s you use, the smaller the heading is (i.e. ### is smaller than ##, which is smaller than #).
- Lists: By placing a dash at the start of a line, and then putting a space before the text, you can created a bulleted list.
    - If you'd rather have the list use numbers, replace the asterisk with a number followed by a period (such as "1. ").
    - Indentation is supported as well.
- Horizontal line: If you want to add a horizontal line to the page, to space elements apart, make a line that only has three dashes ("---").
- Links: Place the text you want to be a link inside square brackets [], and the link itself immediately after in parenthesees ().
    - Example: This link goes to \[Google\]\(https://google.com\)

You can view additional information at [this website](https://www.markdownguide.org/cheat-sheet/), although note that the "Extended Syntax" section is not supported.
