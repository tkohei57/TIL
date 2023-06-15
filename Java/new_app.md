# Javaでのアプリケーション作成手順

## アプリケーションの雛形を生成

※railsではターミナルでrails newコマンドを実行した部分

1.プロジェクトファイルの作成
- Spring Initializrにアクセスして必要な情報を入力し、プロジェクトファイルを作成する。
- 生成されたzipファイルを解凍

2.IntelliJ IDEAでアプリケーションファイル内にあるbuild.gradleを開く

3."アプリ名"Applicationファイルを右クリックして実行
- この際にBad Request 400のようなメッセージが出てしまった場合は、クッキーを消去するか、application.properties内に以下のコードを記述する
```Java
server.max-http-header-size=1MB
```
