# Build A Checkout UpSell App

In this mini lecture we will walk through the steps needed to build and deploy a Shopify app that extends the buyers experience by suggesting additional products to add to their cart prior to checkout.

## Shopify for eCommerce

Shopify is the second most used e-commerce platform worldwide, with 20% of the top 1 million live websites worldwide being powered by Shopify.  It's particularly dominant in the United States and several large and well-known brands use Shopify including Nestle, Pepsi, Unilever, Kylie Cosmetics, Vogue, and Gymshark.




## Shopify Apps

Shopify apps are built on a variety of Shopify tools to create a great merchant experience.  At the time of writing this tutorial there were over 8,000 apps published in the [Shopify App Store](https://apps.shopify.com/), not including all of the custom apps built for specific stores. 

<img src="https://i.imgur.com/j0Gllp7.png"/>

There is also a high demand for Shopify React Developers which makes the combination of Shopify and React skills particularly valuable.

## Creating a Pre-Purchase Product Offer App

This mini lecture is based on Shopify an existing [pre-purchase product offers](https://shopify.dev/docs/apps/checkout/product-offers/pre-purchase) tutorial but also introduces additional tools (which ones? GraphiQL, Theme Editor) and context to help further your understanding of Shopify's tech stack and ecosystem.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 5min

Before we do anything let's take a first take a look at what we will be building and how we can manage our app in the Shopify Theme Editor.

Demo the deployed app and adding/positioning the app in the Theme Editor. 

<hr>

## What you'll learn

In this tutorial, you'll learn how to do the following tasks:

- Create a basic checkout UI extension that renders some text in the checkout flow.

- Run the extension locally and test it on a development store.

- Show an initial loading state for the products to be offered.

- Fetch and filter cart lines from the Storefront API, to display to customers.

- Add a cart line to an order.

- Deploy your extension code to Shopify.


Additionally you will learn:

- To install and use the [Shopify GraphiQL app](https://shopify-graphiql-app.shopifycloud.com/login) within the store Admin
- Position the app at different extension points in the Checkout Theme Editor
- Deploy the app on [Gadget.dev](https://gadget.dev/)

## Requirements
- You've signed up for a free [Gadget.dev](https://gadget.dev/) account.
- You've created a [Partner account](https://www.shopify.com/partners?shpxid=21c96bb0-AE77-4A2A-C167-F82FF6B2649D).

<!-- - You've created a new [development store](https://shopify.dev/docs/apps/tools/development-stores), where you've enabled the [checkout extensibility developer preview](https://shopify.dev/docs/api/release-notes/developer-previews#previewing-new-features).

- You've [populated your store with test products](https://shopify.dev/docs/apps/getting-started/create#step-4-add-and-publish-products-to-your-development-store-for-testing).

- You've [created an app that uses Shopify CLI 3.0 or higher](https://shopify.dev/docs/apps/getting-started/create). -->

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Check-in

Confirm everyone has created a free [Gadget.dev](https://gadget.dev/) account and a [Shopify Partner account](https://www.shopify.com/partners?shpxid=21c96bb0-AE77-4A2A-C167-F82FF6B2649D).

<hr>

## Create A New Shopify Store

In order to work with checkout extensions we need to create a development store with **checkout extensibility developer preview** enabled. 

Login to [shopify.com/partners](https://www.shopify.com/partners) and click on `Add store` button.

<img src="https://i.imgur.com/loYIuYP.png" />

Choose `Create a store to test and build`

<img src="https://i.imgur.com/z8PnG6N.png" />

Give your store a **unique name/url** and choose `Checkout extensibility` from the `Developer Preview` dropdown.

<img src="https://i.imgur.com/yVXCb4n.png" />

Now you will be able to open the store's Admin console.

<img src="https://i.imgur.com/NLtk439.png" />

Under **Sales channels > Online Store** click `View your store`.

<img src="https://i.imgur.com/BknEoQQ.png" />

<!-- Reset the password for your store

<img src="https://i.imgur.com/USqQnW1.png" /> -->

## Create a Shopify App

Back in Shopify Partners click on the `Apps` side navigation link and then click the `Create app` button.

<img src="https://i.imgur.com/6Xh1QPG.png" />

<!-- <img src="https://i.imgur.com/nHGPLcO.png" /> -->

Assign the app a name and click `Create`

<img src="https://i.imgur.com/8gMZiTq.png" />

Once the app is created we will be provided **Client crednetials**, including the `Client ID` and `Client secret`,  both of which we will be needed later when creating a new app on Gadget. 

<img src="https://i.imgur.com/40RAx0l.png" />

<!-- <img src="https://i.imgur.com/pGCRKJW.png" /> -->

## Gadget

1. Login to Gadget.dev
1. Create a new Gadget app (name must be unique in the `gadget.app` namespace.)
2. Click `Click to Shopify` button



<img src="https://i.imgur.com/n0ZYfRx.png" />

Add your Shopify Client ID and Client Secret keys.

<img src="https://i.imgur.com/I3MDMXY.png" />

Connect to Shopify.

<img src="https://i.imgur.com/cT1RGqj.png" />

Choose **Product** for the scope.

<img src="https://i.imgur.com/DGR1QqE.png" />

<img src="https://i.imgur.com/VLWVWHH.png" />

<!-- <img src="https://i.imgur.com/163moSJ.png" /> -->

Copy the App URL and Allowed redirection URL from Gadet to our new Shopify app.

<img src="https://i.imgur.com/qfhtLMu.png" />

Click `Save`

Open app in VSCode and delete the Web folder and then run:

```js
npm run dev
```

Here you will be prompted to choose the Partner Organization

<img src="https://i.imgur.com/I9VtU5X.png" />

And then choose `No, connect it to an existing app`

<img src="https://i.imgur.com/VUVcYL0.png" />

Once the previous steps are completed start the app by running:

```js
npm run dev
```

You will be prompted to install the @shopify/create-app package

<img src="https://i.imgur.com/FSZkboG.png">

Choose **node**

<img src="https://i.imgur.com/94gWC7S.png" />

Assign your app a name.

<img src="https://i.imgur.com/VDgivDX.png" />

Once completed you should see the following success message.

<img src="https://i.imgur.com/S0TJeu2.png" />

Once the previous steps are completed start the app by running:

```js
npm run dev
```

<img src="https://i.imgur.com/DWNgBgz.png">

At this point we can `ctrl + c` to quit as the app won't respond just yet. 

### Create a UI extension

Now that the Shopify Cli has successfully created a project its time to generate an extension.  This requires providing the following info:

1. Type of extension
2. Extension name 
3. What tech will we be building in

Create the extension by running:

```js
npm run shopify app generate extension 
```

<img src="https://i.imgur.com/aUnxoOX.png" />

### Install the app on your store

Click on the app we just built.

<img src="https://i.imgur.com/mXT49c8.png" />

Click the `Select store` button.

<img src="https://i.imgur.com/Rzk2YcR.png" />

Choose your store.

<img src="https://i.imgur.com/K3rHLo1.png" />

<!-- You might be directed to this 

<img src="https://i.imgur.com/3SOGw6m.png" /> -->

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 5min

Provide quick overview of the by reviewing the [Sample Code](https://shopify.dev/docs/apps/checkout/product-offers/pre-purchase/getting-started#sample-code).

<hr>


### Start your local env

Run `npm run dev` to start the local environment.  
<img src="https://i.imgur.com/6rN0LI2.png" />

This will provide a Preview URl so copy/paste that into a new tab to open the` Developer Console`.

<img src="https://i.imgur.com/YzgL6qJ.png" >

Now click `checkout ui extension` to open Shopify Checkout and render the extension. If everything was successful you should see the extension rendered on the top left of the app. 

<img src="https://i.imgur.com/7ppgmXO.png" />

### Import Components

### Set up the extension point

### Fetch products for the offer

### Select which products to offer

### Set up the logic to display an error banner

### Render the components

### Deploy the UI Extension


### Resources
- [Getting started with pre-purchase product offers](https://shopify.dev/docs/apps/checkout/product-offers/pre-purchase/getting-started)