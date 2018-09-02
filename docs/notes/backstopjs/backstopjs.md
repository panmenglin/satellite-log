# BackstopJS 安装

BackstopJS 可以实现多页面、多测试用例测试

github地址：[https://github.com/garris/BackstopJS](https://github.com/garris/BackstopJS)

## 依赖

1. node.js

Node.js (>= v8.9)

npm (>=v6.4)

2. backstopjs

```
npm install -g backstopjs
```

其依赖的 phantomjs 和 Chromium 都会在这个过程中安装

Chromium 安装过程经常会因为网络原因安装失败跳过，虽然也可以后面单独安装，但是需要做关联配置，建议 uninstall backstopjs 重新安装

## 创建测试

使用 init 命令创建一个 backstop 测试

```
backstop init
```

之后会在跟目录生成一个 backstop.json 用于配置测试的配置文件

```json
{
  "id": "backstop_default",
  // 设置不同的屏幕尺寸
  "viewports": [
    {
      "label": "phone",
      "width": 320,
      "height": 480
    },
    {
      "label": "tablet",
      "width": 1024,
      "height": 768
    }
  ],
  "onBeforeScript": "puppet/onBefore.js",
  "onReadyScript": "puppet/onReady.js",
  "scenarios": [
    {
      "label": "BackstopJS Homepage",
      "cookiePath": "backstop_data/engine_scripts/cookies.json",
      "url": "https://garris.github.io/BackstopJS/",
      "referenceUrl": "",
      "readyEvent": "",
      "readySelector": "",
      "delay": 0,
      "hideSelectors": [],
      "removeSelectors": [],
      "hoverSelector": "",
      "clickSelector": "",
      "postInteractionWait": 0,
      "selectors": [],
      "selectorExpansion": true,
      "expect": 0,
      "misMatchThreshold" : 0.1,
      "requireSameDimensions": true
    }
  ],
  "paths": {
    "bitmaps_reference": "backstop_data/bitmaps_reference",
    "bitmaps_test": "backstop_data/bitmaps_test",
    "engine_scripts": "backstop_data/engine_scripts",
    "html_report": "backstop_data/html_report",
    "ci_report": "backstop_data/ci_report"
  },
  "report": ["browser"],
  "engine": "puppeteer",
  "engineOptions": {
    "args": ["--no-sandbox"]
  },
  "asyncCaptureLimit": 5,
  "asyncCompareLimit": 50,
  "debug": false,
  "debugWindow": false
}

```

## 跟设计图对比

按照 backstop.json 中的配置，修改对应尺寸的设计图命名，放到 bitmaps_reference 配置的文件夹目录下

执行 test

```
backstop test
```

## 多个环境对比

可以通配置 referenceUrl 来实现多个环境的对比

1. 根据 referenceUrl 生成对比图

```
backstop reference
```

2. 执行 test

```
backstop test
```

测试之后会生成对应的报告

## 测试报告

默认会在配置的 html_report 目录下生成 html 测试报告

![图片描述](./backstopjs/01.png)

报告中会显示对比的结果，通过率，对比双方的同屏对比图等
