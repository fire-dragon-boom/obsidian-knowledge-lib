## 配置文件

### eslint and prettier

```json5
{
  "editor.formatOnSave": true,

  "editor.codeActionsOnSave": {

    "source.fixAll.eslint": "explicit",

  },

  "editor.defaultFormatter": "esbenp.prettier-vscode",

  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact"],

  "eslint.format.enable": false,

  "prettier.printWidth": 100,

  "prettier.tabWidth": 2,

  "prettier.useTabs": false,

  "prettier.semi": false,

  "prettier.singleQuote": true,

  "prettier.trailingComma": "all",

  "prettier.bracketSpacing": true,

  "prettier.arrowParens": "always",

  "prettier.endOfLine": "lf",
}
```