[![npm](https://img.shields.io/npm/v/@nsoft/vuetify-colorizer.svg)](https://www.npmjs.com/package/@nsoft/vuetify-colorizer) 
[![Greenkeeper badge](https://badges.greenkeeper.io/nsftx/vuetify-colorizer.svg)](https://greenkeeper.io/) 
[![Build Status](https://travis-ci.org/nsftx/vuetify-colorizer.svg?branch=master)](https://travis-ci.org/nsftx/vuetify-colorizer) 
[![codebeat badge](https://codebeat.co/badges/690f689b-87eb-42f4-a656-cc3400ac3c0d)](https://codebeat.co/projects/github-com-nsftx-vuetify-colorizer-master)
[![codecov](https://codecov.io/gh/nsftx/vuetify-colorizer/branch/master/graph/badge.svg)](https://codecov.io/gh/nsftx/vuetify-colorizer)

# vuetify-colorizer

> Color component for Vuetify framework

## Installation

```bash
# npm
npm install @nsoft/vuetify-colorizer
```

## Using

### Import styles

You need to import colorizer style in your main stylesheet file or component. Example of importing in `stylus` file:

```stylus
@import '@nsoft/vuetify-colorizer/dist/vuetify-colorizer.css';
```

### Import script

```javascript
import Vue from 'vue';
import { VColorPickerInput } from '@nsoft/vuetify-colorizer';
import App from './App';

Vue.config.productionTip = false;
Vue.use(VColorPickerInput);

/* eslint-disable no-new */
new Vue({
  el: '#app',
  template: '<App/>',
  components: { App },
});
```

### Import component locally

```javascript
import { VColorPickerInput } from '@nsoft/vuetify-colorizer';

export default {
  name: 'app',
  components: {
    VColorPickerInput,
  },
};
```

### Use in template

```html
<template>
  <div id="app">
    <VColorPickerInput/>
  </div>
</template>
```
