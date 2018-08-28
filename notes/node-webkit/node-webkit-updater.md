# node-webkit 桌面应用的热更新

最近在开发基于 nw.js 的桌面应用，需求中需要实现软件的热更新，下面简单说下实现步骤

## 依赖

### [nw.js](https://nwjs.io/)

node-webkit 相当于 Chromium 和 node.js 的结合体，我们可以通过它来将web应用打包成跨平台的桌面应用，使桌面应用的开发更加简单、高效

### [node-webkit-updater](https://github.com/edjafarov/node-webkit-updater)

由 nw 官方开发者提供的 应用热更新组件

#### 安装

`npm install node-webkit-updater`

## 使用

### 配置文件

修改开发目录下的 `package.json` ，设置版本检查的信息和新版本下载地址

```json
    {
        "name": "应用名",
        "version": "0.0.1", //版本号
        "manifestUrl": "xxx/package.json", //应用需要校验的配置文件地址
        "packages": { //新版本压缩包下载地址
            "mac": {
                "url": "xxx/updapp.zip"
            },
            "win": {
                "url": "xxx/updapp.zip"
            },
            "linux32": {
                "url": "xxx/updapp.tar.gz"
            }
        }
    }
```

### 校验版本

在项目的 js 中使用 `node-webkit-updater` 进行版本校验

```javascript
    var gui = require('nw.gui'); //操作nw应用
    var pkg = require('./package.json'); // 本地配置文件
    var updater = require('node-webkit-updater'); //热更新
    var upd = new updater(pkg);
    var copyPath, execPath;
    var progressTimer; //设置一个定时器，用来模拟下载的进去条
    
    
    
    if (gui.App.argv.length) {
        copyPath = gui.App.argv[0];
        execPath = gui.App.argv[1];
    
        // 替换旧版本
        upd.install(copyPath, function(err) {
            if (!err) {
    
                // 重启
                upd.run(execPath, null);
                gui.App.quit();
            }
        });
    } else {
        // 从manifest目录校验版本
        upd.checkNewVersion(function(error, newVersionExists, manifest) {
            if (!error && newVersionExists) {
                // 有新版本显示下载进度条开始下载
                $('.mask').show();
                setTimeout(function() {
                    var startC = parseInt(Math.floor(Math.random() + 1) * 3);
                    $('.progress div').width(startC + '%');
                    progressTimer = setInterval(function() {
                        startC += Math.random() * 2;
                        if (startC >= 95) {
                            clearInterval(progressTimer);
                            startC = 95;
                        }
                        $('.progress div').width(startC + '%');
                        $('.progress p').html(startC.toFixed(2) + '%');
                    }, 2000);
                }, 1000);
    
    
                // 下载新版本
                upd.download(function(error, filename) {
                    if (!error) {
                        clearInterval(progressTimer);
                        $('.progress div').width('100%');
                        $('.progress p').html('100%');
                        // 下载完成关闭应用
                        upd.unpack(filename, function(error, newAppPath) {
                            if (!error) {
    
                                // 重启应用
                                upd.runInstaller(newAppPath, [upd.getAppPath(), upd.getAppExec()], {});
                                gui.App.quit();
                            }
                        }, manifest);
                    }
                }, manifest);
            }
        });
    }
```

### 更新版本

当有新版本更新后把新版本打成压缩包放到配置文件中配置的目录，

并把新的package.json也放到配置的目录下

这样用户在打开应用的时候就会去校验版本，如果有新版本就会去自动下载了，并且在下载完成后应用会自动重启

