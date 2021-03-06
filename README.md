# [Step 0](https://github.com/locize/react-tutorial/tree/main/step_0) - Starting point
![](https://github.com/locize/react-tutorial/tree/main/img/step_0.jpg)
Let's start with a simple react app bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app) and instrumented with a simple [i18next](https://www.i18next.com/) setup thanks to [react-i18next](https://react.i18next.com/).

The translation files are hosted on the same server where the react app is hosted.

Use `npm run start` to run the app.


# [Step 1](https://github.com/locize/react-tutorial/tree/main/step_1) - keep existing code setup, but synchronize with locize
![](https://github.com/locize/react-tutorial/tree/main/img/step_1.jpg)
Here, you basically keep the existing setup, like in [Step 0](https://github.com/locize/react-tutorial/tree/main/step_0) but are synchronizing the translation files with locize.
This can be done on-demand or on the CI-Server or before deploying the app.

## What to do to reach this step:
1. in locize: signup at https://locize.com/register and [login](https://docs.locize.com/integration/getting-started/create-a-user-account)
2. in locize: [create a new project](https://docs.locize.com/integration/getting-started/add-a-new-project)
3. in locize: add "de" as additional language (this can also be done via [API](https://docs.locize.com/integration/api#add-new-language))
4. install the [locize-cli](https://github.com/locize/locize-cli)

## use the [locize-cli](https://github.com/locize/locize-cli)
Use the `npm run syncLocales` script to synchronize your [local repository](https://github.com/locize/react-tutorial/tree/main/step_1/public/locales) with what is published on locize.

Alternatively, you can also use the `npm run downloadLocales` script to always download the published locize translations to your [local repository](https://github.com/locize/react-tutorial/tree/main/step_1/public/locales) before bundling your app.


# [Step 2](https://github.com/locize/react-tutorial/tree/main/step_2) - use the [locize CDN](https://docs.locize.com/whats-inside/cdn-content-delivery-network)
![](https://github.com/locize/react-tutorial/tree/main/img/step_2.jpg)
Here, the [locize-cli](https://github.com/locize/locize-cli) is not used anymore.
The app will be directly "connected" with locize.

The translations are dynamically fetched from the [locize CDN](https://docs.locize.com/whats-inside/cdn-content-delivery-network).

This means you can change the translations without the need to adapt and deploy your app.

## What to do to reach this step:
1. install [i18next-locize-backend](https://github.com/locize/i18next-locize-backend)
2. adapt the [i18next config](https://github.com/locize/react-tutorial/tree/main/step_2/src/i18n.js), make sure you copy the [project-id](https://github.com/locize/react-tutorial/tree/main/step_2/src/i18n.js#L7) and [api-key](https://github.com/locize/react-tutorial/tree/main/step_2/src/i18n.js#L8) from within your locize project.
3. remove the local locales (i.e. /public/locales)
4. [get the available languages dynamically](https://github.com/locize/react-tutorial/tree/main/step_2/src/App.js#L31) and [render the language switcher accordingly](https://github.com/locize/react-tutorial/tree/main/step_2/src/App.js#L45)

Thanks to the use of the [saveMissing functionality](https://github.com/locize/react-tutorial/tree/main/step_2/src/App.js#L54), new keys gets added to locize automatically, while developing the app.


# [Step 3](https://github.com/locize/react-tutorial/tree/main/step_3) - more locize goodies
![](https://github.com/locize/react-tutorial/tree/main/img/step_3.jpg)
Here, you will add some extra locize goodies to further optimize the localization workflow.

## What to do to reach this step:
1. install the [locize-lastused](https://github.com/locize/locize-lastused) plugin
2. install the [locize](https://github.com/locize/locize) plugin
3. adapt the [i18next config](https://github.com/locize/react-tutorial/tree/main/step_3/src/i18n.js)

Thanks to the [locize-lastused](https://github.com/locize/locize-lastused) plugin, you'll be able to [find and filter in locize which keys are used or not used anymore](https://docs.locize.com/guides-tips-and-tricks/unused-translations).

With the help of the [locize](https://github.com/locize/locize) plugin, you'll be able to use your app within the locize [InContext Editor](https://docs.locize.com/more/incontext-editor).


# [Step 4](https://github.com/locize/react-tutorial/tree/main/step_4) - production version with caching
![](https://github.com/locize/react-tutorial/tree/main/img/step_4.jpg)
Now, we prepare the app for [going to production](https://docs.locize.com/guides-tips-and-tricks/going-production). There is to do just a little [i18next config](https://github.com/locize/react-tutorial/tree/main/step_4/src/i18n.js) change.

## What to do to reach this step:
1. in locize: create a dedicated version for production
2. in locize: Do not enable auto publish for that version and publish manually or via [API]​(https://docs.locize.com/integration/api#publish-version) or via [CLI](https://github.com/locize/locize-cli#publish-version)
3. in locize: [enable Cache-Control max-age​](https://docs.locize.com/more/caching)
4. adapt the [i18next config](https://github.com/locize/react-tutorial/tree/main/step_4/src/i18n.js) to read from environment specific [settings](https://github.com/locize/react-tutorial/tree/main/step_4/.env) ([development](https://github.com/locize/react-tutorial/tree/main/step_4/.env.production) vs. [production](https://github.com/locize/react-tutorial/tree/main/step_4/.env.development))

Now, during development, you'll continue to [save missing keys](https://github.com/locize/react-tutorial/tree/main/step_4/src/i18n.js#L43) and to make use of [lastused feature](https://github.com/locize/react-tutorial/tree/main/step_4/src/i18n.js#L22). => `npm run start`

And in production environment, saveMissing and lastused are disabled, and also the api-key is not exposed. => `npm run build && npm run serve`