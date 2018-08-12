# PowerShellに関するメモ

## ps1スクリプトをローカルで実行するための設定

```
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
```

## 環境変数

### 環境変数の一覧を表示する

```
Get-ChildItem env:
```

### 環境変数を表示する

```
echo $env:環境変数名
```

## ダウンロード

wget的なやつ

```
Invoke-WebRequest -Uri URL -OutFile outputfilename
```


## zip解凍

```
Expand-Archive -Path <圧縮ファイルパス> -DestinationPath <ファイル解凍先フォルダ>
```
