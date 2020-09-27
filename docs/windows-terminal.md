# Windows Terminal + Powershellで使いやすいシェル環境を構築する [更新日：2020/09/27]

大いに参考にさせていただいたブログは、[Windows TerminalとPowerShellでクールなターミナル環境をつくってみた](https://blog.mamansoft.net/2020/05/31/windows-terminal-and-power-shell-makes-beautiful/)
です。

## Windows Terminal

### インストール

Windows Terminalの開発が行われている[Github - microsoft/terminal](https://github.com/microsoft/terminal)のREADMEによると、Microsoft Storeからのインストールが推奨されています。
そのため、公式の推奨に従う形で[Microsoft Store](https://www.microsoft.com/ja-jp/p/windows-terminal/9n0dx20hk701)からインストールします。

### 設定

Windows Terminalの設定はタイトルバー右の`∨`マークから設定を選択、もしくは`Ctrl+,`で開く`settings.json`に記載します。
設定項目は次のドキュメントで公開されています。

* プロファイルの設定に関係なく、ターミナル ウィンドウ全体に影響するもの
    * [Windows ターミナルでのグローバル設定](https://docs.microsoft.com/ja-jp/windows/terminal/customize-settings/global-settings)
    * これらは、`settings.json`ファイルのルートに配置する必要があります。
* それぞれ一意のプロファイルに固有のもの
    * [Windows ターミナルでのプロファイル設定](https://docs.microsoft.com/ja-jp/windows/terminal/customize-settings/profile-settings)
    * 設定を自分のすべてのプロファイルに適用する場合は、ご自分の settings.json ファイル内のプロファイルの一覧の上にある`defaults`セクションに追加できます。

## PowerShell

### インストール

クロスプラットフォーム対応の`PowerShell Core`をインストールします。

公式Githubリポジトリ[PowerShell/PowerShell](https://github.com/PowerShell/PowerShell)のREADMEに、プラットフォーム毎のインストーラへのDownloadリンクがあります。

インストーラに従えばすぐインストールできます。私は右クリックで開くオプションのみonとしています。

### Powerlineの設定

Microsoftドキュメント[チュートリアル: Windows ターミナルで Powerline をセットアップする](https://docs.microsoft.com/ja-jp/windows/terminal/tutorials/powerline-setup)の通りに実施します。

### bashのキーバインドを使用できるようにする

```powershell
Set-PSReadLineOption -EditMode Emacs
```
