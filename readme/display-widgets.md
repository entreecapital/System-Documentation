# Display widgets

This page walks you through all available _display_ widgets settings.

For an introduction on what widgets are and a comprehensive list of what widgets you'll be able to choose from, check out the previous page: [Customize your fields](https://docs.forestadmin.com/developer-guide/reference-guide/fields/customize-your-fields)​

This is the most basic way to display your content (depending on your field type). If you want to take into account text formatting, check out the next section.

With this widget, you can control how your dates will be displayed:

To customize your date format, use [momentjs](https://momentjs.com/) syntax:

This widget allows you to display a number as a nicely formatted price:

* Choose a currency symbol between **euros** (EUR), **dollars** (USD) and **pounds** (GBP)
* Choose a base: **Cents** if your values are stored in cents, **Unit** otherwise

The **number formatting** is based on your browser's locale, unless you have a specific [locale](<../.gitbook/assets/general tab>) set in your Project settings.

This widget is useful to display a number (ranged between 0 and 1) as a percentage.

Without using the percentage widget:

Using the percentage widget:

If you manually **search** for a percentage value, you should type the unformatted value, as shown below.

This widget is your go-to widget for viewing files of all types.

Previews are only available for images and PDFs.

Images can be previewed from all views. Click on them to display the following modal:

From this modal, you can:

* **Drag & drop** your zoomed-in area

The _File viewer_ widget will also act as a **carousel** when viewing multiple images or files. In this case, your field must be defined as an array of strings (`type: ['String']`).

Your images need to be **public** to be displayed! If you must keep them **private**, you should consider using [signed URLs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-signed-urls.html).

From the table view, clicking on the file icon will open the PDF in a new tab.

From the summary and details views, the PDF can be previewed:

If your PDF seems to be loading indefinitely, it might be protected (you'll see a `Load denied by X-Frame-Options` error in your console).

This can be solved by adding

`X-Frame-Options: ALLOW-FROM https://app.forestadmin.com/`

in your file hosting server (replace `https://app.forestadmin.com` by your custom domain if you have one).

In this widget's settings, you can manage whether to authorize rotation and zoom features, add a prefix and change the preview size.

Use this option to specify a URL prefix or path prefix depending on your usage. For instance:

* If you store your files on an external cloud (ie: AWS S3) and in your database as a **filename**, your prefix will be a link like this:
* If you store your images in **base64**, you could find it convenient to add a `data:image/png;base64` prefix on the go:

Choosing a preview size will show your image or PDF in the following sizes:

Small (max-height: 150px)

Medium (max-height: 400px)

Large (max-height: 1000px)

_Custom_ allows you to specify a precise height and width in pixels.

Select this widget if your content is actually URLs.

Links will always **open in a new tab**.

Note that if your content is not a valid url, it will still be clickable but simply show a blank page. You can also choose to display a title instead of the link.

Select this widget if you want to visualize a point coordinates on a map.

Coordinates format must be: - 48.8566, 2.3522 - 48.8566° N, 2.3522° E

Use this widget to neatly display your JSON.
