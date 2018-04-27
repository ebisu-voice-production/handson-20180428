# Lesson 03 メモアプリを考え、実装してみよう
## Lesson 02の振り返り
Echoアプリで学んだことでは、ユーザーが発話した内容を単発的に処理することしか出来ませんでした。  
入力に対して、対応する出力を返すだけなので、例えば質問とそれに回答するような単純なものは作ることはできますが、話題を継続する様なことは出来ません。  
会話の流れ（文脈）や前回のアプリ使用後の内容について対応できれば、幅の広いアプリを作ることができます。

## メモアプリで目指すもの
音声でメモを残すことの出来るアプリを考え、実装しましょう。このレッスンでは前回のような写経ではなく、自由に作ることを目標にします。  
メモアプリの基本機能として考えられるのは、
- 記録
- 参照
- 削除
でしょうか。
さらに、仕組みをシンプルに考えるとして、UX的にはどうでしょう。左をユーザー、右をアプリの発話内容としてみると以下のような感じでしょうか。

### 記録する場合
- 1. （アプリ起動）- 「こんにちは、どうしますか？」
- 2. 「メモを記録」- 「メモを記録します、内容を教えてください。」
- 3. 「卵を買う」- 「「卵を買う」を記録しておきますね。ではまた。」

### 参照し、聞き終わったら削除する場合
- 1. （アプリ起動）- 「こんにちは、どうしますか？メモは1件あります。」（記録しているメモ数を教えてあげると嬉しい？）
- 2. 「メモを参照」- 「「卵を買う」とメモがありました。このメモを削除しますか？」
- 3-a. 「はい」- 「削除しました。ではまた。」
- 3-b. 「いいえ」- 「まだ削除しないでおきますね、ではまた。」

## 必要な機能
[公式リファレンス](https://actions-on-google.github.io/actions-on-google-nodejs/classes/actionssdk.actionssdkconversation.html)  
- [dataプロパティ](https://actions-on-google.github.io/actions-on-google-nodejs/classes/actionssdk.actionssdkconversation.html#data): アプリ起動〜終了の間(セッション)で保持したいデータをJSON形式で持っています。実際はobjectとして扱えます
- [userプロパティ](https://actions-on-google.github.io/actions-on-google-nodejs/classes/conversation.user.html): ユーザー単位でGoogle側が保持するデータです
  - [storageプロパティ](https://actions-on-google.github.io/actions-on-google-nodejs/classes/conversation.user.html#storage): セッションを超えて保持したいデータをJSON形式で扱えます。実際はobjectとして扱えます。

## 参考例
上記の実装例としてサンプルを用意したのでヒントとしてください。  
[GitHub](https://github.com/ebisu-voice-production/actions-sdk-example-memo)  
[ZIP](https://github.com/ebisu-voice-production/actions-sdk-example-memo/archive/master.zip)

## 発展課題
もっと使いやすくなるように自由に改造してみましょう、例えば以下のような内容にチャレンジしてみてください。
- 初めてアプリを使う場合と次回以降の起動メッセージを切り替えられるようにする
  - 例）初回起動時に使い方を丁寧に説明し、次回以降は簡潔な内容にする
- メモの登録後や参照後に終了せずに続けて命令できるようにする
  - 例）「〜〜を記録しておきますね、他に何かありますか？」など
- メモを柔軟に参照できるようにする
  - 例）連続で聞けるようにする、検索できるようにする
