# React17 + React Hook + TS4 + json-server

## 创建 TS 项目

npx create-react-app [name] --template typescript

## 运行项目

npm start

## 配置 git commit 提交规范

是否符合规范，如果不符合则不允许提交

1、[安装 Prettier](https://prettier.io/docs/en/install.html)

- `npm install --save-dev --save-exact prettier`

- 然后，创建一个空的配置文件，以使编辑器和其他工具知道您正在使用 Prettier：`echo {}> .prettierrc.json`

- 接下来，创建一个.prettierignore 文件，让 Prettier CLI 和编辑器知道哪些文件不格式化。这是一个例子：
  ````js
  # Ignore artifacts:
   build
   coverage
   ```
  2、[Pre-commit Hook](https://prettier.io/docs/en/precommit.html)
  ````

> 注意使用 husky 之前，必须先将代码放到 git 仓库中，否则本地没有.git 文件，就没有地方去继承钩子了。

当您想与 Prettier 一起使用其他代码质量工具（例如 ESLint，Stylelint 等）或需要支持部分暂存文件（git add --patch）时很有用。

devDependencies 在继续操作之前，请确保已安装 Prettier 并在其中。

```js
npx mrm lint-staged
```

这将安装 husky 和 lint-staged，然后在项目的配置中添加一个配置，该配置 package.json 将在预提交挂钩中自动格式化支持的文件。

pageage.json 配置

```js
"lint-staged": {
    "*.{js,css,md,ts,tsx}": "prettier --write"
  }
```

3、[安装 eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)

- `npm install --save-dev eslint-config-prettier`

- pageage.json 配置

  ```js
  "eslintConfig": {
      "extends": [
        "react-app",
        "react-app/jest",
        "prettier" // 增加prettier，覆盖之前一部分规则
      ]
    },
  ```

4、[安装 json-server](https://github.com/typicode/json-server)
`npm i json-server -g`

完全遵循 reset api 风格，可在 postman 里做增删改查

- 根目录新建一个**json-server-mock**/db.json
- 启动 json-server `json-server --watch db.json`
- package.json 增加一项 script：

  `"json-server": "json-server __json-server-mock__/db.json --watch"`

  执行`npm run json-server`启动试试
