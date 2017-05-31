# Tarayıcıda TypeScript
Web uygulaması yaratmak için TypeScript kullanıyorsanız önereceklerim şunlardır:

## Genel Makine Kurulumu

* [NodeJS](https://nodejs.org/en/download/) yüklenir.

## Proje Kurulumu
* Proje yolu oluşturulur.
```
mkdir proje-adi
cd proje-adi
```
* `tsconfig.json` dosyası oluşturulur. Modülleri [ayrıca](../project/external-modules.md) tartışacağız. Bunu oluşturmanın başka bir nedeni de 'tsx' derlemesinde gerekli olduğu içindir.
```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true,
        "jsx": "react"
    },
    "exclude": [
        "node_modules"
    ],
    "compileOnSave": false
}
```
* Npm projesi oluşturulur:
```
npm init -y
```
* TypeScript-nightly, webpack, [`ts-loader`](https://github.com/TypeStrong/ts-loader/), typings yüklenir.
```
npm install typescript@next webpack ts-loader typings --save-dev
```
* Typings başlatılır (sizin için bir typings.json dosyası yaratır).
```
"./node_modules/.bin/typings" init
```
* Tüm kaynaklarınızı içeren tek bir `bundle.js` dosyasına modüllerinizi paketlemek için` webpack.config.js` dosyası oluşturulur: 
```js
module.exports = {
    entry: './src/app.tsx',
    output: {
        path: './build',  
        filename: 'bundle.js'
    },
    resolve: {
        // Add `.ts` and `.tsx` as a resolvable extension.
        extensions: ['', '.webpack.js', '.web.js', '.ts', '.tsx', '.js']
    },
    module: {
        loaders: [
            // all files with a `.ts` or `.tsx` extension will be handled by `ts-loader`
            { test: /\.tsx?$/, loader: 'ts-loader' }
        ]
    }
}
```
* Bir yapı çalıştırmak için bir npm komut dosyası kurun. Ayrıca `npm install` üzerinde` typings install` çalıştırın. `Package.json` dosyanıza` script` bölümü ekleyin:
```json
"scripts": {
    "prepublish": "typings install",
    "watch": "webpack --watch"
},
```

Şimdi sadece bu komutu çalıştırın. (`webpack.config.js`'nin olduğu konumunda çalıştırılması gerekir):

```
npm run watch
```

Şimdi eğer `ts` veya `tsx` dosyasında değişiklik yaparsanız webpack sizin için `bundle.js` dosyası oluşuturacaktır. Web sunucunuz ile bunu sunabilirsiniz.

## Fazlası
Eğer React kullanacaksanız (ki ben kesinlikle bir bakmanızı tavsiye ediyorum) yapılacak birkaç adım daha var:

```
npm install react react-dom --save-dev
```

```
"./node_modules/.bin/typings" install dt~react --global --save
```

```
"./node_modules/.bin/typings" install dt~react-dom --global --save
```

Demo olarak `index.html`:
```
<html>
    <head>
        <meta charset="UTF-8" />
        <title>Hello React!</title>
    </head>
    <body>
        <div id="root"></div>

        <!-- Main -->
        <script src="./dist/bundle.js"></script>
    </body>
</html>
```
Demo olarak `./src/app.tsx`
```ts
import * as React from "react";
import * as ReactDOM from "react-dom";

const Hello = (props: { compiler: string, framework: string }) => {
    return (
        <div>
            <div>{props.compiler}</div>
            <div>{props.framework}</div>
        </div>
    );
}

ReactDOM.render(
    <Hello compiler="TypeScript" framework="React" />,
    document.getElementById("root")
);
```

Bu demo projeyi buradan klonlayabilirsiniz : https://github.com/basarat/react-typescript

## Canlı Yeniden Yükleme (Live Reload)

Kolaylıkla webpack developer sunucusu eklenir: 

* Yükleme : `npm install webpack-dev-server` 
* `package.json` içine ekleme : `"start":"webpack-dev-server --hot --inline --no-info --content-base ./build"`

Şimdi `npm start`komutunu çalıştırınca bu artık canlı yeniden yükleme işini yapabilen webpack dev sunucusunu başlatacaktır.
