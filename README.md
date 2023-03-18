# golang-hands-on

📗「Go言語ハンズオン」(著:掌田津耶乃)のサンプルコード (※Chapter4のみ)

## このリポジトリについて

このリポジトリでは、Chapter4のサンプルコードを[fyne v2](https://developer.fyne.io/)に対応させています。  
fyne v2の変更点については[こちらの情報](https://developer.fyne.io/api/v2.0/upgrading)を参考にしています。

## 始め方

### 0. goとgccのインストール

※ 詳しくは書籍の情報をご参照ください。

### 1. モジュールの作成とfyne v2関連パッケージの取得

```shell
cd golang-hands-on
go mod init myapp
go get fyne.io/fyne/v2...
```

### 2. main.goに実行したいコードを入力

※ `ch4_codes.md`に各種サンプルコードを記載しています。

### 3. main.goの実行

```shell
go run main.go
```