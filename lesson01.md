# Lesson 01
## 公式ガイド
[https://developers.google.com/actions/extending-the-assistant](https://developers.google.com/actions/extending-the-assistant)

## 開発準備
- Google アカウントの用意、Action用プロジェクトの[作成](https://console.actions.google.com/)
- Node.js (v6.11.5) の[インストール](https://nodejs.org/en/blog/release/v6.11.5/)
- gactions CLIの[インストール](https://developers.google.com/actions/tools/gactions-cli)

### Action用プロジェクトの作成
アプリケーションを作成するにはプロジェクトが必要です。  
新規でアプリケーションを作る際はまずプロジェクトを作成しましょう。
- Actions on Googleコンソールの[トップページ](https://console.actions.google.com/)で、「Add/Import project」をクリック
- Project nameを任意の英数字で入力(※ただし、プロジェクトIDが必ず指定した文字列と完全に一致しない場合もあるので注意。例えば、echoと入力しても、echo-7b403などとなる場合もある)
- Country/regionを設定

### gactions CLIの設定(Linux, Mac)
- PATHの通ってる場所にgactionsを移動(例えば`/usr/local/bin`)(`~/.bash_profile`や`~/.bashrc`で確認もしくは追加)
- `$ chmod +x gactions` で実行権限付与
