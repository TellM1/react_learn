# About React 

### Reactとは
- Facebook社開発のUIライブラリー
- UI作成においてcomponentという概念が特徴としてある
- componentの組み合わせによってwebPageを作成していく
- 仮想DOMによって従来のツリー構造の画面描画より効率的な動作をする。
    - Javascriptのオブジェクトとして扱うことでブラウザへの負荷を減らしjs engineのメモリを使用する。
- DOMの状態をjsで管理することができ、状態を持つUIとされている
- 既存の描画との差分を認識することができるため必要な部分だけを描画する差分描画できる

### JSXについて
- JSの拡張言語とされている。
- HTMLをそのまま書き込むことができる + JSの構文が使える
- jsxは最終敵にReact要素を生成するため
- フルスクラッチで書いたHTMLと結果的には同じものが表示できるように書くことが前提
- React.createElementで生成処理をすることでhtmlを生成できている
- React.create~~構文は直感的にかけずjsxにすることで楽に開発ができる
- jsx基本文法規則
    1. Reactライブラリーをimportする
    2. return文の中がjsxの構文になる 
    3. *class は className
    4. 変数に関してはキャメルケースが前提 凸凹でつなぎ目をわかりやすくするやつ！
    5. タグの最後に閉じタグが必要である
    6. 変数記述には{}波カッコでかこう必要性がある
    7. jsxは必ず階層構造であることが必要
    8. React.Fragmentで囲うことで階層化を作ることができる htmlタグとして出力されないため〇
    9. <></>で省略形で描ける
```
import React from 'react';

const pushBtn = () =>{
    var url = '******.com';

    return(
        <React.Fragment>
            <!-- 以下の部分に画面に返すHTML記述 -->
            <button className={'push_btn'}>
                push!
            </button>
            <!-- 最後の〆たぐ -->
            <img href={url} />
        </React.Fragment>
    )
}
export default pushBtn
```

### 実際の開発に向けて導入
- create-react-app
    - 簡単にReactの開発環境を構築できる
    - 本来はreact環境構築は設定が必要だったりする
        - トランスパイラーのBabel 
        - バンドら―のWebpack
        <!-- 初学者向けではないため飛ばしたい -->
    - Nodejs : 10.16以上
    - npm : 5.6 以上
    - 導入コマンドは[npx create-react-app myapp]
    - myappは自分のファイル名
```
<!-- npm系でのコマンド一覧  -->
npm start (appを起動)
npm run build (デプロイ用のコマンド　一つのファイルにまとめる作業をしてくれる)
npm run eject (webpackなどの設定を変更したいとき用)
```


    