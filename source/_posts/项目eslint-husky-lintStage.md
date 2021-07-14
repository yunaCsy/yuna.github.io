---
title: 前端项目使用工具规范代码
date: 2021-07-14
tags: 
---

# Eslint

[Eslint](https://eslint.bootcss.com/docs/rules/) **是在 js 代码**中识别和报告模式匹配**的工具**，他的目标是保证代码的一致性和避免错误。

Eslint 的主要功能包含代码格式的校验，代码质量的校验，js 规范。在实际项目中 Eslint 可以检测出代码问题，并标红，但是并不会自动格式化，需要手动格式化。

1. `yarn add eslint`
2. `yarn run eslint --init`（自动生成.eslintrc 配置文件,）
   - 这一步会有几个问题，按照项目需求选择即可
   - 如安装失败(如还需安装那个插件)，按照失败的提示修改即可
3. vscode: settings.json 配置。
4. eslint 规则 配置到.eslintrc 文件中

```json
// 添加 settings.json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": [
    "react",
    "html",
    "javascript",
    "typescript",
    "javascriptreact",
    "typescriptreact"
  ]
}
```

此时，在项目目录 ctrl+shift+p 输入 eslint，确保 eslint 已经启用了，此时保存时 eslint 就可以自动检测代码了，像双引号还可以自动修复为单引号。

# Git Hooks

Git 也具有在特定事件发生之前或之后执行特定脚本代码功能（从概念上类比，就与监听事件、触发器之类的东西类似）。[Git Hooks](https://www.cnblogs.com/jiaoshou/p/12222665.html) **就是在哪些 git 执行特定事件后触发运行的脚本**。默认情况下 hooks 目录是.git/hooks,但是可以通过 core.hookPath 配置变量来更改。

项目初始化的时候会生成默认钩子(脚本大多是 shell 和 Perl 语言的)，包含大部分可以使用的钩子，但是.sample 扩展名防止他们默认被执行。

因为 hooks 是本地的，不会 git clone 到仓库，也不会收版本控制影响。

# husky

[husky](https://typicode.github.io/husky/#/) 是一个 git Hook 工具。

husky 使用 git 的一个新功能 core.hookPath 指定 git hooks 所在的目录而不是使用默认的.git/hooks/。

使用 husky install 将 git hooks 的目录指定为.husky/。使用 husky add 命令向.husky/中添加 hook。通过这种方式我们就可以只添加我们需要的 git hook，而且所有的脚本都保存在了一个地方（.husky/目录下）因此也就不存在同步文件的问题了。

1. `yarn add husky -d`
2. 启用 Git 钩子 `npx husky install`
3. 要在安装后自动启用 Git 挂钩，请编辑 package.json

   prepare 脚本会在 npm install（不带参数）之后自动执行。也就是说当我们执行 npm install 安装完项目依赖后会执行 husky install 命令，该命令会创建.husky/目录并指定该目录为 git hooks 所在的目录。

```json
// package.json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```

4. 创建一个钩子
   使用 husky add <file> [cmd]（不要忘记 husky install 之前运行）

```
npx husky add .husky/pre-commit "yarn start"
git add .husky/pre-commit
```

[husky 版本区别](https://blog.csdn.net/qq_21567385/article/details/116429214)

# lint-staged

[lint-staged](https://github.com/okonet/lint-staged) 仅仅是过滤器(仅过滤 git 暂存文件)，不会帮你格式化任何东西，所以没有代码规则配置文件，需要自己配置一下，如：.eslintrc、.stylelintrc 等，然后在 package.json 中引入。

当文件变化，我们 git commit 它们，pre-commit 钩子会启动，执行 lint-staged 命令，我们对于 lint-staged 如上文配置，对本次被 commited 中的所有.js 文件，执行 eslint --fix 命令和 git add,命令，前者的的目的是格式化，后者是对格式化之后的代码重新提交。

1. `yarn add lint-staged -d`
2. 配置 lint-staged.config.js 文件

```js
// lint-staged.config.js
module.exports = {
  // 在 git 的待提交的文件中，在 src 目录下的所有 js,json,ts,tsx 都要执行两条命令。第一条eslint --cache(仅仅检查改变过的文件) 和--fix ，后一条是将处理过的代码重新 add 到 git 中。
  "src/**/*.{js,json,ts,tsx}": [
    "eslint --cache --fix",
    "git add",
  ],
  "src/**/*.{*}": ["git add"],
};
```
