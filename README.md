# 01

```bash
    npm inti -f
    git init
    git add .
    git commit -m 'first commit'
    git remot add origin git@github.com:xx/xx.git
    git push -u orgin master
```
eslint

```bash
    ./node_modules/.bin/eslint --init
```

[eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)


# 02

```json
  "scripts": {
    "lint:js": "eslint *.js",
    "lint:css": "stylelint *.less",
    "lint:json": "jsonlint --quiet *.json",
    "lint:markdown": "markdownlint --config .markdownlint.json *.md",
    "test": "mocha tests/"
  },
```

```json
      "test": "npm run lint:js && npm run lint:css && npm run lint:json && npm run lint:markdown && mocha tests/"
```

```json
    "test": "npm run lint:js & npm run lint:css & npm run lint:json & npm run lint:markdown & mocha tests/"
```

```json
    "test": "npm run lint:js & npm run lint:css & npm run lint:json & npm run lint:markdown & mocha tests/ &wait"
```


```npm-run-all```

```json

"test": "npm-run-all lint:js lint:css lint:json lint:markdown mocha"


"test": "npm-run-all lint:* mocha"

```

# 03

```json
    "//": "运行所有代码检查和单元测试",
```

```bash
    npm test -s[--silent][--loglevel silent]
```

```bash
    npm test -d[--verbose][--loglevel verbose]
```

# 04

```bash
    npm run env
    npm run env | grep npm_package | sort
```

```shell
    "echo":"echo $npm_package_name"

```

```json

    "cover:cleanup": "rm -rf coverage && rm -rf .nyc_output",

    "cover:archive": "mkdir -p coverage_archive/$npm_package_version && cp -r coverage/* coverage_archive/$npm_package_version",

    "postcover": "npm run cover:archive && npm run cover:cleanup && opn coverage_archive/$npm_package_version/index.html",
    
```

# 05

```bash

    npm i rimraf cpr make-dir-cli -D
```

```json

  "scripts": {
-    "cover:cleanup": "rm -rf coverage && rm -rf .nyc_output",
-    "cover:archive": "cross-var \"mkdir -p coverage_archive/$npm_package_version && cp -r coverage/* coverage_archive/$npm_package_version\"",
+    "cover:cleanup": "rimraf coverage && rimraf .nyc_output",
+    "cover:archive": "cross-var \"make-dir coverage_archive/$npm_package_version && cpr coverage/* coverage_archive/$npm_package_version -o\"",
     "cover:serve": "cross-var http-server coverage_archive/$npm_package_version -p $npm_package_config_port",
     "cover:open": "cross-var opn http://localhost:$npm_package_config_port",
-    "postcover": "npm-run-all cover:archive cover:cleanup --parallel cover:serve cover:open"
+    "precover": "npm run cover:cleanup",
+    "postcover": "npm-run-all cover:archive --parallel cover:serve cover:open"
  },
```


```bash
    npm i cross-var -D
    # npm install cross-var --save-dev
    # yarn add cross-var -D
```
```json
"scripts": {
     "cover:cleanup": "rm -rf coverage && rm -rf .nyc_output",
-    "cover:archive": "mkdir -p coverage_archive/$npm_package_version && cp -r coverage/* coverage_archive/$npm_package_version",
-    "cover:serve": "http-server coverage_archive/$npm_package_version -p $npm_package_config_port",
-    "cover:open": "opn http://localhost:$npm_package_config_port",
+    "cover:archive": "cross-var \"mkdir -p coverage_archive/$npm_package_version && cp -r coverage/* coverage_archive/$npm_package_version\"",
+    "cover:serve": "cross-var http-server coverage_archive/$npm_package_version -p $npm_package_config_port",
+    "cover:open": "cross-var opn http://localhost:$npm_package_config_port",
     "postcover": "npm-run-all cover:archive cover:cleanup --parallel cover:serve cover:open"
   },

```

```bash
npm i cross-env -D
# npm install cross-env --save-dev
# yarn add cross-env -D
```

```json
  "scripts": {
-    "test": "NODE_ENV=test mocha tests/",
+    "test": "cross-env NODE_ENV=test mocha tests/",
  },
```
