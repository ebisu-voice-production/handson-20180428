# Lesson 02 Echoサンプル
## Echoサンプルで目指すもの
起動後、ユーザーの発話した内容をそのまま返すシンプルなものを実装します。  
終了する場合は、終了用のキーワードで終了出来るようにしましょう。  
`src/index.js`を編集していきます。

## 準備
- Echoアプリのプロジェクトを新規作成
- テンプレートとなるファイル群を[ダウンロード](https://github.com/ebisu-voice-production/actions-sdk-example-echo/archive/starter.zip)
- プロジェクト内で`$ npm install`し、必要なパッケージをインストール

## コーディング
[actions-on-google](https://github.com/actions-on-google/actions-on-google-nodejs)と[firebase-functions](https://github.com/firebase/firebase-functions)が必要となるので2つをインポート。  
ActionsSdkAppのリファレンスは[コチラ](https://developers.google.com/actions/reference/nodejs/ActionsSdkApp)
```
const ActionsSdkApp = require('actions-on-google').ActionsSdkApp;
const functions = require('firebase-functions');
```

Actions on Googleアプリ、echoアプリのエンドポイントとなるexport関数を定義。
```
exports.echo = functions.https.onRequest((request, response) => {
});
```

処理を振り分ける目安となるintent2つの為のactionMapを設定。  
ひとまず、`actions.intent.MAIN`は、起動時。`actions.intent.TEXT`はそれ以外と受け止めてください。
```
exports.echo = functions.https.onRequest((request, response) => {
  const app = new ActionsSdkApp({ request, response });
  const actionMap = new Map();
  actionMap.set('actions.intent.MAIN', mainIntent); // mainIntentは処理用関数
  actionMap.set('actions.intent.TEXT', rawInput); // rawInputは処理用関数
  app.handleRequest(actionMap);
});
```

起動時にechoアプリに喋らせたい内容を記述。
```
const mainIntent = app => {
  app.ask(/* 喋らせたい内容 */); // ask関数は会話を続けたい場合に使用
};
```

起動後のユーザーの発話を処理する内容を記述。
```
const rawInput = app => {
  const rawInput = app.getRawInput(); // getRawInput関数はユーザーの発言内容をテキスト化したものを取得
  if (/* アプリ終了用の条件式 */) {
    app.tell(/* 終了時に喋らせたい内容 */);
  } else {
    app.ask(/* エコーされたとわかるような内容 */);
  }
};
```

完成コードの例
```
const ActionsSdkApp = require('actions-on-google').ActionsSdkApp;
const functions = require('firebase-functions');

const mainIntent = app => {
  app.ask('Hi! Can you say something? You can finish this conversation to say bye.');
};
const rawInput = app => {
  const rawInput = app.getRawInput();
  if (rawInput === 'bye') {
    app.tell('Goodbye!');
  } else {
    app.ask(`You said, ${rawInput}. Can you say something?`);
  }
};

exports.echo = functions.https.onRequest((request, response) => {
  const app = new ActionsSdkApp({ request, response });
  const actionMap = new Map();
  actionMap.set('actions.intent.MAIN', mainIntent);
  actionMap.set('actions.intent.TEXT', rawInput);
  app.handleRequest(actionMap);
});
```

## echo関数をデプロイ
- `$ npm run firebase -- login`で、デプロイしたいアカウントでログイン
- `$ npm run firebase -- use --add [YOUR_PROJECT]` YOUR_PROJECTを新規作成したプロジェクトIDに変えて実行
- `$ npm run deploy`で、デプロイ

## action.jsonの作成とActionのデプロイ
- `action.template.json`を元に、LOCALEとYOUR_ENDPOINT_URLを設定
  - 日本語の場合は、LOCALEをjaに変更（英語の場合は、enもしくは、localeプロパティ自体を削除）
  - YOUR_ENDPOINT_URLは、`$ npm run deploy`でデプロイしたecho関数のエンドポイントURLに変更
- `$ PROJECT=[YOUR_PROJECT] npm run deploy-action` YOUR_PROJECTを新規作成したプロジェクトIDに変えて実行

## シミュレータで動作確認
- [コンソール](https://console.actions.google.com/)から作成したプロジェクトに移動し、プロジェクトのSimulatorでアプリを作動させて動作確認
- Languageをaction.jsonで指定したものに設定（localeを削除した場合はEnglishでOK）

## Firebaseコンソールでecho関数のログ確認
- ソースコード中に何かしらconsole.log()を記述した場合、[コンソール](https://console.actions.google.com/)から作成したプロジェクトに移動し、プロジェクトのBackend services > Cloud Functions(> View in Firebase)内で確認が可能
