### Install Angular ESLint
`ng add @angular-eslint/schematics`


### Install Prettier and Prettier-ESLint dependencies
`npm install prettier prettier-eslint eslint-config-prettier eslint-plugin-prettier --save-dev `

### Install additional plugins
`npm i eslint-plugin-import eslint-plugin-jsdoc eslint-plugin-prefer-arrow eslint-plugin-unused-imports eslint-plugin-import-newlines  —save-dev `

### ESLint configuration
Filename: `.eslintrc.json`
```json
{
  "root": true,
  "overrides": [
    {
      "files": [
        "*.ts"
      ],
      "plugins": [
        "import",
        "unused-imports",
        "prettier"
      ],
      "parserOptions": {
        "project": [
          "tsconfig.json",
          "e2e/tsconfig.json"
        ],
        "createDefaultProgram": true
      },
      "extends": [
        "plugin:@angular-eslint/recommended",
        "plugin:@angular-eslint/ng-cli-compat",
        "plugin:@angular-eslint/ng-cli-compat--formatting-add-on",
        "plugin:@angular-eslint/template/process-inline-templates",
        "prettier"
      ],
      "rules": {
        "prettier/prettier": "error",
        "@typescript-eslint/member-ordering": "off",
        "@typescript-eslint/explicit-member-accessibility": [
          "error",
          {
            "overrides": {
              "accessors": "no-public",
              "constructors": "no-public",
              "methods": "no-public",
              "properties": "no-public"
            }
          }
        ],
        "@typescript-eslint/indent": [
          "error",
          2,
          {
            "ignoredNodes": [
              "TemplateLiteral"
            ]
          }
        ],
        "@angular-eslint/component-selector": [
          "error",
          {
            "type": "element",
            "prefix": "app",
            "style": "kebab-case"
          }
        ],
        "@angular-eslint/directive-class-suffix": "off",
        "@angular-eslint/directive-selector": [
          "error",
          {
            "type": "attribute",
            "prefix": "app",
            "style": "camelCase"
          }
        ],
        "arrow-parens": [
          "off",
          "always"
        ],
        "comma-dangle": [
          "error",
          "always-multiline"
        ],
        "quotes": [
          "error",
          "single",
          {
            "avoidEscape": true
          }
        ],
        "no-multiple-empty-lines": [
          2,
          {
            "max": 1,
            "maxEOF": 0
          }
        ],
        "no-unused-vars": "off",
        "unused-imports/no-unused-imports": "error",
        "unused-imports/no-unused-vars": [
          "warn",
          {
            "vars": "all",
            "varsIgnorePattern": "^_",
            "args": "after-used",
            "argsIgnorePattern": "^_"
          }
        ],
        "import/no-duplicates": [
          "error",
          {
            "considerQueryString": true
          }
        ],
        "import/order": [
          "error",
          {
            "newlines-between": "always",
            "groups": [
              "external",
              "builtin",
              "internal",
              "sibling",
              "parent",
              "index"
            ],
            "pathGroups": [
              {
                "pattern": "@environments/*",
                "group": "internal"
              },
              {
                "pattern": "@helpers",
                "group": "internal"
              },
              {
                "pattern": "@helpers/**",
                "group": "internal"
              },
              ....
              // describe all alias from tsconfig paths in project for correct import order
            ],
            "pathGroupsExcludedImportTypes": [
              "internal"
            ],
            "alphabetize": {
              "order": "asc",
              "caseInsensitive": true
            }
          }
        ],
        "object-curly-spacing": [
          "error",
          "never"
        ],
        "no-empty-function": "off",
        "@typescript-eslint/no-empty-function": "warn",
        "@angular-eslint/no-empty-lifecycle-method": "warn"
      }
    },
    {
      "files": [
        "*.html"
      ],
      "extends": [
        "plugin:prettier/recommended",
        "plugin:@angular-eslint/template/recommended"
      ],
      "rules": {
        "prettier/prettier": [
          "error",
          {
            "parser": "angular",
            "bracketSameLine": true,
            "bracketSpacing": false,
            "htmlWhitespaceSensitivity": "strict"
          }
        ]
      }
    }
  ]
}

```
Filename: `.eslintignore`
```
projects/**/*
node_modules/**/*
.angular
dist
e2e
```


### Prettier Configuration
Filename: `.prettierrc`
```json
{
  "printWidth": 120,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "all",
  "arrowParens": "always",
  "bracketSameLine": false,
  "overrides": [
    {
      "files": "*.html",
      "options": {
        "parser": "angular",
        "bracketSameLine": true,
        "bracketSpacing": false,
        "htmlWhitespaceSensitivity": "strict"
      }
    },
    {
      "files": "*.scss",
      "options": {
        "parser": "scss",
        "trailingComma": "none"
      }
    },
    {
      "files": "*.css",
      "options": {
        "parser": "css",
        "trailingComma": "none"
      }
    },
    {
      "files": "*.json",
      "options": {
        "parser": "json",
        "trailingComma": "none"
      }
    }
  ]
}


```

Filename: `.prettierignore`
```
projects/**/*
node_modules/**/*
.angular
dist
e2e

# Ignore files
*.ts
```


### angular.json config 

```json
"lint": {
  "builder": "@angular-eslint/builder:lint",
  "options": {
    "lintFilePatterns": [
      "src/**/*.ts",
      "src/**/*.html"
    ]
  }
},
```

### old angular version
For old angular version need downgrade eslint dev dependcies. Example for v12:
````
  "eslint": "^7.26.0",
  "eslint-config-prettier": "^8.5.0",
  "eslint-plugin-import": "^2.10.0",
  "eslint-plugin-jsdoc": "^39.3.6",
  "eslint-plugin-prefer-arrow": "^1.2.3",
  "eslint-plugin-prettier": "^4.2.1",
  "eslint-plugin-unused-imports": "^1.1.5",
````


### VSCode extensions:
// need test config for vs code, copied from other article
```
dbaeumer.vscode-eslint
esbenp.prettier-vscode
```

### Add the following to your .vscode/settings.json file:
```
{
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    "editor.formatOnSave": false
  },
  "[typescript]": {
    // "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.defaultFormatter": "dbaeumer.vscode-eslint",
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    "editor.formatOnSave": false
  },
},
"editor.suggest.snippetsPreventQuickSuggestions": false,
"editor.inlineSuggest.enabled": true
```

### Webstorm settings
1. Go to Preferences -> Languages & Frameworks -> Javascript -> Prettier 
2. Set glob pattern for files `{**/*,*}.{html, scss,css}` and checkbox on 'Reformat code' action 
![image](https://user-images.githubusercontent.com/25185920/193795536-a54f12dc-ec3f-4f28-9f0b-8c7c7a75194b.png)

3. Add actions on save
![image](https://user-images.githubusercontent.com/25185920/193795865-8c7f3aca-657d-4c4f-8e7a-e72a19231d5d.png)


### Add Fix Lint and Prettier errors command in package.json
`"lint": "ng lint --fix"`

