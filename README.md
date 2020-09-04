# Marking Cloud CodeLab

## リポジトリについて

このリポジトリは[Codelabs Site](https://github.com/googlecodelabs/tools/tree/master/site)をカスタマイズしたものです。

build結果をdocsにリネームすることで[GitHub Pagesで公開](https://docs.github.com/ja/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#choosing-a-publishing-source)できるようにしています。

## コンテンツのデプロイ方法

以下の流れで新しいコンテンツをデプロイできます。

1. [環境を整える](#環境を整える)
2. [コンテンツを作成する](#コンテンツを作成する)
3. [codelabs/に追加する](#codelabsに追加する)
4. [デプロイする](#デプロイする)
5. [GitHub Pagesから確認](#github-pagesから確認)

### 環境を整える

Node.jsとGo(とclaat)が使える環境が必要です。
以下がインストール済みか確認してください。

- [Go](https://golang.org/dl/) language
- [Node.js](https://nodejs.org/en/download/) v10+ and [npm](https://www.npmjs.com/get-npm)
- [claat](https://github.com/googlecodelabs/tools/tree/master/claat#install)

### コンテンツを作成する

Google Documentでコンテンツを作成します。

- [公式サンプル](https://docs.google.com/document/d/1E6XMcdTexh5O8JwGy42SY3Ehzi8gOfUGiqTiUX6N04o/edit)
- [公式フォーマットガイド](https://github.com/googlecodelabs/tools/blob/master/FORMAT-GUIDE.md)

[Preview Codelab](https://chrome.google.com/webstore/detail/preview-codelab/lhojjnijnkiglhkggagbapfonpdlinji)でプレビューしながら作ることができます。

### codelabs/に追加する

リポジトリをクローンします。

```
git clone https://github.com/kou72/kou72.github.io.git
cd kou72.github.io.git/
```

codelabs/ に移動してcodelab形式のHTMLファイルを生成します。

```
cd codelabs/
claat export <GoogleDocumentID>
cd ../
```

### デプロイする

npm install で必要なパッケージを取得します

```
npm install
```
npm run deploy でデプロイ(=push)します。

```
npm run deploy
```

npm run deploy の中身はこんな感じです。

```
  "scripts": {
    "build": "npx gulp dist --codelabs-dir=codelabs",
    "docs": "rm -rf docs/ && mv dist docs && rm docs/codelabs && cp -r codelabs docs/codelabs",
    "push": "git add -A && timestamp=$(date \"+%Y%m%d-%H%M%S\") && git commit -m \"automated commited $timestamp\" && git push origin HEAD",
    "deploy": "run-s build docs push"
  },
```

### GitHub Pagesから確認

[GitHub Pages](https://kou72.github.io/)が変更されたらデプロイ完了です！

デプロイ結果が反映されるのに少し時間がかかります。
