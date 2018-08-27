# 统一的 commit message 规范

借助一系列 commit message 规范化工具统一 message 的格式和内容，并通过 git hook 实现对 commit message 的合规检查, 达到统一提交备注规范的目的


1. 首先全局安装 commitizen

```
sudo npm install -g commitizen
```

借助 @commitizen/cz-cli 提供的 git cz 命令来替代 git commit 命令


2. 项目目录安装 cz-customizable

```
npm install --save-dev cz-customizable
```
通过 cz-customizable 我们可以自定义 commit message 规范

修改 package.json

```json
···

"config": {
  "commitizen": {
    "path": "node_modules/cz-customizable"
  }
}

···
```

同时在项目目录下创建 .cz-config.js, 维护需要的格式

3. 项目目录安装 commitlint 相关

```
npm install --save-dev @commitlint/cli
```

```
npm install --save-dev @commitlint/config-conventional
```

用来进行 commit message 内容检查


4. 项目目录安装 commitlint-config-cz

```
npm install --save-dev commitlint-config-cz
```

并在项目跟目录创建 .commitlintrc.js 进行校验配置

```json
module.exports = {
  extends: [
    '@commitlint/config-conventional',
  ],
  rules: {
    'subject-case': [0],
  }
};
```

5. 项目目录安装 husky 借助 git hook 在 commit message 时对内容进行检查

```
npm install --save-dev husky 
```

package.json 配置 hook

```json
···

"husky": {
  "hooks": {
    "commit-msg": "commitlint -e $GIT_PARAMS"
  }
}

···
```

6. 通过 standard-version 自动生成 CHANGELOG

```
npm install --save-dev standard-version
```

package.json 中配置命令


```json
···

"scripts": {
  "changelog": "standard-version"
}

···
```

就可以通过 npm run changelog 来生成变更日志了