---
title: react eslint配置
tags:
  - eslint
  - react
categories: 开发工具
description: react eslint基础配置
abbrlink: d32fe85b
top_img: https://yuminjun.oss-cn-hangzhou.aliyuncs.com/zelda/5.jpg
cover: https://yuminjun.oss-cn-hangzhou.aliyuncs.com/zelda/5.jpg
date: 2019-4-15
---

#### react eslint配置
```
{
  "env": {
    "browser": true,
    "es6": true,
    "node": true
  },
  "extends": [
    "standard",
    "eslint:recommended",
    "react-app"
  ],
  "globals": {
    "Atomics": "readonly",
    "SharedArrayBuffer": "readonly"
  },
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    },
    "ecmaVersion": 2018,
    "sourceType": "module"
  },
  "rules": {
    "semi": [
      "error",
      "always"
    ],
    "quotes": [
      "error",
      "single",
      {
        "avoidEscape": true
      }
    ],
    "space-before-function-paren": "off",
    "no-console": "off"
  }
}
```

//.eslintignore
```
/config
/node_modules
/scripts
```