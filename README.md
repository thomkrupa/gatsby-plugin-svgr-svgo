# gatsby-plugin-svgr-svgo

Plugin allows you to use SVGs as react components, configure SVGO(SVG optimization) settings and declare rules for SVG url loader with or without optimization.

## Install

```
npm install gatsby-plugin-svgr-svgo @svgr/webpack --save
```
## Setup 

### Default configuration
Add to your gatsby-config.js

```js
plugins: [
  `gatsby-plugin-svgr-svgo`
]
```
By default there are two rules will be added:
1. SVG as a react component(innline svg), SVGO enabled for all SVGs that have .inline postfix. Example: ``cat.inline.svg``
```js
import React from 'react';
import CatInlineSvg from '../images/cat.inline.svg';


const IndexPage = () => (
  <div>
    <CatInlineSvg />
  </div>
);

export default IndexPage;

```

2. SVG as a file that available by url, SVGO enabled for all svgs that have ``.svg``. Example: ``cat.svg``.

```js
import React from 'react';
import CatSvg from '../images/cat.svg';


const IndexPage = () => (
  <div>
    <img src={CatSvg} />
  </div>
);

export default IndexPage;

```

### Advanced configuration

```js
plugins: [
    {
      resolve: 'gatsby-plugin-svgr-svgo',
      options: {
        inlineSvgOptions: [
          {
            test: /\.inline.svg$/,
            svgoConfig: {
              plugins: [{
                removeViewBox: false,
              }],
            },
          },
        ],
        urlSvgOptions: [
          {
            test: /\.svg$/,
            svgoConfig: {
              plugins: [{
                removeViewBox: false,
              }],
            },
          },
        ],
      },
    }
]
```
You can decalre various rules based on loader that should be used under ``inlineSvgOptions`` and ```urlSvgOptions```.

``test`` - pattern that will be used to match file name

``svgoConfig`` - accepts plugins list with settings, list of available plugins(options) you can find [here](https://github.com/svg/svgo#what-it-can-do)

``svgo`` - disables SVGO if set in ``false``

### SVGO disabled example:

```js
plugins: [
    {
      resolve: 'gatsby-plugin-svgr-svgo',
      options: {
        urlSvgOptions: [
          {
            test: /\.svg$/,
            svgo: false,
          },
        ],
      },
    }
]
```
