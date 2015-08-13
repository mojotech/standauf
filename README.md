![](https://d13yacurqjgara.cloudfront.net/users/111934/screenshots/2192403/attachments/404994/attachment.png)

### Development workflow

#### Serve / watch

```sh
npm run start
```

This outputs an IP address you can use to locally test and another that can be used on devices connected to your network.

#### Run tests

```sh
npm test
```

This runs the unit tests defined in the `app/test` directory through [web-component-tester](https://github.com/Polymer/web-component-tester).

#### Build & Vulcanize

```sh
npm build
```

Build and optimize the current project, ready for deployment. This includes linting as well as vulcanization, image, script, stylesheet and HTML optimization and minification.

#### Development flow

In order to guarantee that the latest version of your Service Worker script is being used, follow these instructions:

* After you made changes to your service worker script, close all but one of the tabs pointing to your web application
* Hit shift-reload to bypass the service worker as to ensure that the remaining tab isn't under the control of a service worker
* Hit reload to let the newer version of the Service Worker control the page.

If you find anything to still be stale, you can also try navigating to `chrome:serviceworker-internals` (in Chrome), finding the relevant Service Worker entry for your application and clicking 'Unregister' before refreshing your app. This will (of course) only clear it from the local development machine. If you have already deployed to production then further work will be necessary to remove it from your user's machines.

#### Disable Service Worker support after you enabled it

If for any reason you need to disable Service Worker support after previously enabling it, you can remove it from your Polymer Starter Kit project using these 4 steps:

1. Remove references to the platinum-sw elements from your application [index](https://github.com/PolymerElements/polymer-starter-kit/blob/master/app/index.html).
2. Remove the two Platinum Service Worker elements (platinum-sw/..) in [app/elements/elements.html](https://github.com/PolymerElements/polymer-starter-kit/blob/master/app/elements/elements.html)
3. Remove 'precache' from the list in the 'default' gulp task ([gulpfile.js](https://github.com/PolymerElements/polymer-starter-kit/blob/master/gulpfile.js))
4. Navigate to `chrome://serviceworker-internals` and unregister any Service Workers registered by Polymer Starter Kit for your app just in case there's a copy of it cached.

## Frequently Asked Questions

### Where do I configure routes in my application?

This can be done via [`app/elements/routing.html`](https://github.com/PolymerElements/polymer-starter-kit/blob/master/app/elements/routing.html). We use Page.js for routing and new routes
can be defined in this import. We then toggle which `<iron-pages>` page to display based on the [selected](https://github.com/PolymerElements/polymer-starter-kit/blob/master/app/index.html#L105) route.

### How do I add new JavaScript files to Starter Kit so they're picked up by the build process?

At the bottom of `app/index.html`, you will find a build block that can be used to include additional
scripts for your app. Build blocks are just normal script tags that are wrapped in a HTML
comment that indicates where to concatenate and minify their final contents to.

Below, we've added in `script2.js` and `script3.js` to this block. The line
`<!-- build:js scripts/app.js -->` specifies that these scripts will be squashed into `scripts/app.js`
during a build.

```html
<!-- build:js scripts/app.js -->
<script src="scripts/app.js"></script>
<script src="scripts/script2.js"></script>
<script src="scripts/script3.js"></script>
<!-- endbuild-->
```

If you are not using the build-blocks, but still wish for additional files (e.g scripts or stylesheets) to be included in the final `dist` directory, you will need to either copy these files as part of the gulpfile.js build process (see the `copy` task for how to automate this) or manually copy the files.
