---
title: "【Shopify】カスタマイズ画面で変更した色をCSSファイルで扱う方法"
emoji: "💭"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [shopify,css,liquid,scss]
published: true
---
Shopifyテーマのカスタマイズ画面で変更した色をCSSファイルで扱うための方法について、テーマDawnを例に紹介します。
カスタマイズ画面では、以下の画像のようにボタンなどの色などを自由に変更できます。
![](https://storage.googleapis.com/zenn-user-upload/f567dbd69ce669b4c4c5c835.png)
![](https://storage.googleapis.com/zenn-user-upload/7a3f99f2042e0677b5836527.png)

本投稿では、画像内で色を変更した「アクセント1」の部分について、カスタマイズ画面とCSSの関係を記述します。

「アクセント1」のコードは`config/settings_schema.json`に書かれています。カスタマイズ画面で色を変更すると以下のコードの値が変更されます。ここで`label`,`info`はカスタマイズ画面に表示させる文字が設定されています。また、色の初期設定は#121212となっています。
```json:config/settings_schema.json
   {
        "type": "color",
        "id": "colors_accent",
        "default": "#121212",
        "label": "アクセントカラー",
        "info": "サイト内のタグなどの色を変更します"
     }
```

カスタマイズ画面で変更した色をCSSで使用するためには`layout/theme.liquid`の<head>タグ内に以下のコードを書き込む必要があります。
```liquid:layout/theme.liquid
:root {
    --colors_accent: {{ settings.colors_accent }};
}
```
設定した`--colors_accent`をCSSファイル内で以下のように使用することでカスタマイズ画面で変更した色を反映させることができます。

```css:style.css
.btn {
  color: var(--colors_accent);
}
```
---
## 補足
shopifyではスタイルシートの読み込み速度が遅いことからSCSSの使用が非推奨となっています。
https://www.shopify.jp/blog/partner-theme-sass-depricated
しかし、テーマ開発をする上でSCSSは欠かせない存在です。実際には、SCSSをCSSに変換して読み込ませることになると思います。SCSSを使用して開発を行う場合は、次のようにscssファイル内の変数に設定することで扱いやすいコードが書けると思います。
```scss:
$color_accent: var(--colors_accent);
```