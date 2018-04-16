# Lesson 01
## 公式ガイド
[https://developers.google.com/actions/extending-the-assistant](https://developers.google.com/actions/extending-the-assistant)

## 開発準備
- 教材の[ダウンロード](https://github.com/ebisu-voice-production/actions-sdk-example-echo/archive/starter.zip)
- Google アカウントの用意、Action用プロジェクトの[作成](https://console.actions.google.com/)
- Node.js (v6.11.5) の[インストール](https://nodejs.org/en/blog/release/v6.11.5/)
- gactions CLIの[インストール](https://developers.google.com/actions/tools/gactions-cli)

### Action用プロジェクトの作成
- Actions on Googleコンソールの[トップページ](https://console.actions.google.com/)で、「Add/Import project」をクリック
- Project nameを任意の英数字で入力(echo, sample-echoなど)(※ただし、プロジェクト名が必ず指定した文字列と完全に一致しない場合もあるので注意。例えば、echoとした場合、echo-7b403などとなる場合もある)
- Country/regionをJapanに指定

### gactions CLIの設定(Linux, Mac)
- PATHの通ってる場所にgactionsを移動(例えば`/usr/local/bin`)(`~/.bash_profile`や`~/.bashrc`で確認もしくは追加)
- `$ chmod +x gactions` で実行権限付与
