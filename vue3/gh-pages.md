# gh-pages

## 1. Create Repository
`https://github.com/robertleroy/PROJECT_NAME`

<br>

## 2. Commit project
```js
git add .
git commit -m 'first commit'
git remote add origin https://github.com/robertleroy/PROJECT_NAME.git
git push -u origin master
```

<br>

## 3. Create `vue.config.js` in project root folder
``` js
module.exports = {
  publicPath: process.env.NODE_ENV === 'production'
    ? '/PROJECT_NAME/'
    : '/'
}
```

<br>

## 4. Create `deploy.sh` in project root folder
``` js
# abort on errors
set -e

# build
npm run build

# navigate into the build output directory
cd dist

# if you are deploying to a custom domain
# echo 'www.example.com' > CNAME

git init
git add -A
git commit -m 'deploy'

# if you are deploying to https://robertleroy.github.io
# git push -f git@github.com:robertleroy/robertleroy.github.io.git master


///  USE THIS ONE ///   ///  USE THIS ONE ///    ///  USE THIS ONE ///
# if you are deploying to https://robertleroy.github.io/PROJECT_NAME   
# git push -f git@github.com:robertleroy/PROJECT_NAME.git master:gh-pages

git push -f https://github.com/robertleroy/PROJECT_NAME.git master:gh-pages

cd -
```

<br>

## 5. Run `deploy.sh` to deploy
``` js
./deploy.sh
```
