# Vue 3 Lottie

[![npm](https://img.shields.io/npm/v/vue3-lottie)](https://www.npmjs.com/package/vue3-lottie) [![Downloads](https://img.shields.io/npm/dt/vue3-lottie)](https://www.npmjs.com/package/vue3-lottie) [![Stars](https://img.shields.io/github/stars/megasanjay/vue3-lottie.svg?style=flat-square)](https://github.com/megasanjay/vue3-lottie/stargazers) [![License](https://img.shields.io/npm/l/vue3-lottie)](https://github.com/megasanjay/vue3-lottie/blob/main/LICENSE) [![GitHub issues](https://img.shields.io/github/issues/megasanjay/vue3-lottie)](https://github.com/megasanjay/vue3-lottie/issues)

`vue3-lottie` was created to help developers add Lottie animations to their Vue 3 applications. In my search for a simple way to add Lottie animations to my Vue application I found a suprising lack of maintained solutions. `vue3-lottie` is a vue wrapper around the `lottie-web` library with a few additional features.

# Demos

View the live demos here: [https://vue3-lottie.vercel.app](https://vue3-lottie.vercel.app)

# Upgrade to v2.x

If you are using version 1.x of `vue3-lottie` you should upgrade to version 2.x. You can do this by running the [Installation and Usage](#installation-and-usage) command below. This adds TS support for the component. There are some new imports so take a look at the [new documentation](https://vue3-lottie.vercel.app/guide.html#usage).

# Upgrade to v3.x

Remove importing css, upgrade to version 3.x.

# Installation and Usage

## Vue 3

- You can install `vue3-lottie` over `yarn`, `npm` or `pnpm`. `lottie-web` is a dependency of `vue3-lottie` and should be automatically installed when you install `vue3-lottie`.

```sh
# npm
npm install vue3-lottie@latest --save

# yarn
yarn add vue3-lottie@latest

# pnpm
pnpm add vue3-lottie
```

- Register the component in your Vue 3 application.

The most common use case is to register the component globally.

```js
// main.js
import { createApp } from 'vue'
import Vue3Lottie from 'vue3-lottie'

createApp(App).use(Vue3Lottie).mount('#app')
```

To define global components for [Volar type-checking](https://github.com/johnsoncodehk/volar/tree/master/extensions/vscode-vue-language-features#usage) you will need to add:

```ts
// components.d.ts
declare module '@vue/runtime-core' {
  export interface GlobalComponents {
    LottieAnimation: typeof import('vue3-lottie')['Vue3Lottie']
  }
}
export {}
```

If needed rename component to use:

```ts
app.use(Vue3Lottie, { name: 'LottieAnimation' }) // use in template <LottieAnimation />
```

- `name` string (default: 'Vue3Lottie') - set custom component name

Alternatively you can also import the component locally.

```js
import { Vue3Lottie } from 'vue3-lottie'
import 'vue3-lottie/dist/style.css'

export default {
  components: {
    Vue3Lottie,
  },
}
```

You can then use the component in your template

```vue
<template>
  <Vue3Lottie :animationData="AstronautJSON" :height="200" :width="200" />
</template>

<script>
import { Vue3Lottie } from 'vue3-lottie'
import 'vue3-lottie/dist/style.css'

import AstronautJSON from './astronaut.json'

export default {
  components: {
    Vue3Lottie,
  },
  data() {
    return {
      AstronautJSON,
    }
  },
}
</script>
```

## Nuxt 3

This is still experimental. Will be updated soon.

- You can install `vue3-lottie` over `yarn` or `npm`. `lottie-web` is a dependency of `vue3-lottie` and should be automatically installed when you install `vue3-lottie`.

If you are using npm:

```shell
npm install vue3-lottie@latest --save
```

If you are using yarn:

```shell
yarn add vue3-lottie@latest
```

- Create a folder called **`plugins`** at the root of your project.
- Create a file named **`Vue3Lottie.client.ts`** inside the _plugins_ directory.
- Add the following code to the **`Vue3Lottie.client.ts`** file.

```ts
import Vue3Lottie from 'vue3-lottie'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(Vue3Lottie)
})
```

This should register as a global component that you can call anywhere in your app under the <Vue3Lottie> tag.

I would recommend using a `<client-only>` parent tag to ensure that the animation only loads in on the client side.

```vue
<client-only>
  <Vue3Lottie
    animationLink="https://assets10.lottiefiles.com/packages/lf20_soCRuE.json"
    :height="200"
    :width="200"
  />
</client-only>
```

- Import the css file required by the component into your **`app.vue`** file.

```js
import 'vue3-lottie/dist/style.css'
```

# Props and options

More detailed explanations are provided in the [documentation](https://vue3-lottie.vercel.app/guide.html).

| Prop             | Type                                                                                                                                              | Default Value | Description                                                                                                                                                                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| animationData    | Object \| String                                                                                                                                  | ''            | The lottie animation data provided as a JSON or String JSON                                                                                                                                              |
| animationLink    | String                                                                                                                                            | ''            | A URL link to the Lottie animation data (eg: `Lottie Animation URL` on lottiefiles.com)                                                                                                                  |
| width            | Number \| String                                                                                                                                  | "100%"        | Width of the lottie animation container (Numbers correspond to pixel values)                                                                                                                             |
| height           | Number \| String                                                                                                                                  | "100%"        | Height of the lottie animation container (Numbers correspond to pixel values)                                                                                                                            |
| speed            | Number                                                                                                                                            | "1"           | Speed of the lottie animation                                                                                                                                                                            |
| direction        | String                                                                                                                                            | "forward"     | Animation play direction                                                                                                                                                                                 |
| loop             | Number or Boolean                                                                                                                                 | true          | The number of instances that the lottie animation should run (true is infinite)                                                                                                                          |
| autoPlay         | Boolean                                                                                                                                           | true          | Start animation on component load                                                                                                                                                                        |
| delay            | Number                                                                                                                                            | 0             | Delay the animation play state by some milliseconds                                                                                                                                                      |
| pauseAnimation   | Boolean                                                                                                                                           | false         | Prop to pass reactive variables so that you can control animation pause and play                                                                                                                         |
| pauseOnHover     | Boolean                                                                                                                                           | false         | Whether to pause the animation on hover                                                                                                                                                                  |
| playOnHover      | Boolean                                                                                                                                           | false         | Whether to play the animation when you hover                                                                                                                                                             |
| backgroundColor  | String                                                                                                                                            | transparent   | Background color of the container                                                                                                                                                                        |
| rendererSettings | Object                                                                                                                                            | {}            | Options for if you want to use an existing canvas to draw (can be ignored on most cases)                                                                                                                 |
| fetchOptions     | [Object](https://microsoft.github.io/PowerBI-JavaScript/interfaces/_node_modules_typedoc_node_modules_typescript_lib_lib_dom_d_.requestinit.html) | undefined     | Options for fetch request `animationLink` for support additional features like AbortController, credentials, headers and etc... [MDN](https://developer.mozilla.org/en-US/docs/Web/API/fetch#parameters) |

We can use `LottieProps` to define options interface.

```ts
import type { LottieProps } from 'vue3-lottie'
```

# Events

A few events are emitted from the component. Look at the [Demos](#Demos) for examples.

- onComplete
  - If your animation has a finite amount of loops you can use this event to know when the animation has completed.
- onLoopComplete
  - If your animation has a finite amount of loops you can use this event to know when the animation has completed a loop.
- onEnterFrame
  - This event is fired every frame of the animation. There will be 60 events fired per second if your lottie animation runs at 60fps.
- onSegmentStart
  - This event is fired when the animation enters a segment.
- onAnimationLoaded
  - This event is fired when the animation has loaded. This should let you know when you can start referencing the methods for the component.

# Methods

You can control the animation with the following methods. These methods can be called by assigning a `ref` value to the `vue3-lottie` component. Look at the [Demos](#Demos) for examples.

- play
  - Plays the animation
- pause
  - Pauses the animation
- stop
  - Stops the animation. This will also reset the animation to the first frame. Look at the demo for some examples.
- destroy
  - You can call this method to destroy the animation. It will remove the animation from the DOM.
- setSpeed(speed)
  - You can call this method to change the speed of your animation.
- setDirection(direction)
  - You can call this method to change the direction of your animation.
- getDuration(inFrames)
  - You can call this method to get the duration of your animation.
- goToAndStop(frameNumber, isFrames)
  - You can call this method to go to a specific frame of your animation. The animation will be stopped at the end of this call.
- goToAndPlay(frameNumber, isFrames)
  - You can call this method to go to a specific frame of your animation. The animation will be played from this frame.
- playSegments(segments, forceFlag)
  - You can call this method to play a specific segment of your animation.
- setSubFrame(subFrame)
  - You can call this method to set the subframe value.
- updateDocumentData(documentData, index)
  - This method updates text on text layers. Refer to the [official docs](https://github.com/airbnb/lottie-web/wiki/TextLayer.updateDocumentData) for how to use this method.

# Credits

A big thank you goes to [@reslear](https://github.com/reslear) for adding Typescript support to this library. Go check out his profile and give him a follow!

- [@DamianGlowala](https://github.com/DamianGlowala) - PR [#29](https://github.com/megasanjay/vue3-lottie/pull/29) - Fix `watch` function

![forthebadge](https://forthebadge.com/images/badges/made-with-vue.svg) ![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)
