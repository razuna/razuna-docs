**Razuna Extension for Magento**

With the Razuna Magento Extension you can server all your product images in your Magento webshop directly from Razuna.
___
**Download and Installation**

Please note that once you install the extension, you can no longer use product images from Magento directly. The extension will simply ignore product images in Magento and fetch them all from Razuna.In order for the extension to work, you need to have a Razuna instance, which is online. You can use any Razuna deployment: open source, cloud based or enterprise.

The extension uses the default template, which means that if you have a custom template, you need to manually edit the following two files:

app/design/frontend/{package_name}/{theme_name}/template/catalog/product/view/list.phtml
app/design/frontend/{package_name}/{theme_name}/template/catalog/product/view/product/media.phtml

You can install the extension using Magento Connecto Manager in two ways:

1) Through the Magento Community (Extension key: razuna)

2) [By downloding the Magento Package here and uploading it in Magento Connect Manager](http://razunademo.padma.razuna.org/index.cfm?fa=c.sf&f=67FAABFC418A41A2A8E4F2EA3EB54BD8&v=o)

Once installed, you can log out of Magento Admin and back in, and the Extension is ready.

![](/Razuna_tools/img/image201411.png)
___
**Configuration**

You first need to connect your Magento webshop with Razuna. This is simply done in Magento Admin by clicking on System -> Configuration. In the left menu bar you will see "Razuna Configuration", which you click on. This brings up the window below, where you need to fill in the URL or your Razuna instance and your API key. You can also decide which folder, the extension should check. If this is left out, the extension will search all of your Razuna files.

![](/Razuna_tools/img/image201412.png)
___
**Usage**

Once you have clicked "Test API Configuration" and received the "Success" message, you are good to go. Magento will now automatically fetch product images from Razuna and thus ignore any product images you have stored in Magento. So before activating the extension, we suggest you have already tagged your images in Razuna.

The connection between Magento and Razuna is quite simple, allowing you to quickly add and change images for all your products.

What happens is that Magento connects to Razuna and asks for images, where the label in Razuna matches the SKU in Magento. If found, it will present the images along with the product. You can add as many images to the same SKU as you wish. You can also by using the labels "Thumbnail" and "Main" in Razuna decidem, which image to show in the category view and which image to use as main product image.

**Magento**: You don't need to do anything.

**Razuna**: 

1) Upload image(s)

2) Label image with SKU from Magento

3) Label the image, you want to use for the category with additional label: Thumbnail

4) Label the image, you want to use as the main product image with additional label: Main

5) The same image can be used as thumbnail and main image

___

**Create product in Magento**

Below is the steps for a product with SKU c30 in Magento.

![](/Razuna_tools/img/image201413.png)

Note that the Images should not be uploaded as the Razuna Magento extension ignores them anyway.

![](/Razuna_tools/img/image201414.png)

___

**Create labels in Razuna**

![](/Razuna_tools/img/image201415.png)

___

**Add labels to the image directly**

![](/Razuna_tools/img/image201416.png)

___

**Add labels using the Batch feature**

![](/Razuna_tools/img/image201417.png)

___

**Add labels using Export Metadata**

![](/Razuna_tools/img/image201418.png)

___

**Demo**

[Watch the demo on http://magento.razuna.org](http://magento.razuna.org/)

___

**Video**

[Watch this video for a complete overview of the Razuna extension for Magento](http://magento.razuna.org/razuna-magento-manual)



