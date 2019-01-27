# 功能   

## 一、格式化commit message

### 1. 安装 commitizen 依赖包

> npm i commitizen -D

### 2. 在 package.json 中加入以下内容

```json
{
  ...
  "config": {
    "commitizen": {
      "path": "./node_modules/wii-changelog/dist/cz"
    }
  },
}
```

### 3. 在 package.json 中创建以下 script 命令

```json
{
  "cz": "git add . && git cz"
}
```

## 二、生成changelog

### 1. 安装 conventional-changelog-cli 依赖包

```js
npm i conventional-changelog-cli -D
```

### 2. 创建以下命令

```json
{
  ...
  "script": {
    "changelog": "conventional-changelog --config node_modules/wii-changelog/lib/log -i CHANGELOG.md -s -r 0",
  }
}
```
1. 生成当前版本的变化情况
2. 生成所有的日志文件

## 三、lint 模块

### 1. 安装 husky commitlint 依赖

```shall
npm i husky commitlint -D
```

### 2. 在 package.json 中引入以下配置。

```json
{
  ...
  "husky": {
    "hooks": {
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
}
```

### 3. 在项目根路径下创建 .commitlint.js 或者 commitlint.config.js

配置参考：

```js
module.exports = {
  rules: {
    'body-leading-blank': [2, 'always'],
    'footer-leading-blank': [1, 'always'],
    'header-max-length': [2, 'always', 100],
    'subject-empty': [2, 'never'],
    'type-empty': [2, 'never'],
    'type-enum': [2, 'always',
      [
        '新功能',
        '修复',
        ...
      ]
    ],
    'scope-enum': [2, 'always',
      [
        'components/Button',
        '组件/按钮',
      ]
    ]
  }
}
```

## 版本管理使用方法

### 1. 安装 standard-version 依赖包

```js
npm i standard-version -D
```

### 2. 在 package.json 里配置脚本

```json
{
  ...
  "script": {
    "release-major": "standard-version -r major",
    "release-minor": "standard-version -r minor",
    "release-patch": "standard-version -r patch"
  }
}
major: 通常代表一个大的版本更新(1.0.0 -> 2.0.0)
minor: 代表一个小的版本更新(1.0.0 -> 1.1.0)
patch: 代表 bug 修复(1.0.0 -> 1.0.1)
```

> 每次提交会自动更新 changelog 文件