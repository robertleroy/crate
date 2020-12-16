# gh-pages

Simplest way to do this is with [vue-cli-plugin-gh-pages](https://github.com/JaZo/vue-cli-plugin-gh-pages)

## 1. Create Repository
`https://github.com/robertleroy/PROJECT_NAME`

<br>

## 2. Commit project
```js
git init
git add .
git commit -m 'first commit'
git remote add origin https://github.com/robertleroy/PROJECT_NAME.git
git push -u origin master
```

<br>

## 3. Add & run plugin
``` js
vue add gh-pages
npm run gh-pages
```

<br>

Thats it.

[vue-cli-plugin-gh-pages](https://github.com/JaZo/vue-cli-plugin-gh-pages)
