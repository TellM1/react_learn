# About React 
&
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

### コンポーネント概念について
- 見た目と機能を持つUI部品
- 基本は二種類のコンポ
    - Class Component (クラスコンポーネント) 
    - Functional Component (ファンクション　コンポーネント)

```jsx:ComponentSample

// class component
import React,{Component} from 'react';

class header extends Component {
    render(){
        return <><img href="#" className="icon" /></>
    }
}

export default header;

// function component
import React,{Component} from 'react';

class header = () => {
    return (
        <>
            <img href="#" className="icon" />
        </>
    )
}

export default header;

```
- 記述量が違う/propsというあ値渡しの機能もある
- コンポーネントを使う理由
    - 再利用するために(recycle)
    - コードを見やすくし点検効率を上げるため
        - 1つのパーツにつき1ファイル
        - 別ファイル管理にすることでコードが見やすい
    - 変更の際に修正箇所を少なくするため
- app.jsに関しては通常のfunction宣言 compornents/???に関してはアロー関数を用いる。 

### props
```component
const Article = (props) => {
    return (
        <div>
            <h2>{props.title}</h2>
            <p>{props.content}</p>
        </div>
    );
};

export default Article

```

```App.jsx
import Article from "./components/Article";

function App(){
    return(
        <div>
            <Article
                title = {"タイトルサンプル"}
                content = {"内容について"}
            />
        </div>
    );
}

export default App;
```

- 値を引数にpropsを指定する。

### モジュール機能について
- プログラムをモジュールという単位で分割する。
- 原則は1ファイル1モジュール

1. default export (名前なしexport)
    - 推奨されている形
    - 1ファイル　1export 
    - 1度宣言したアロー関数をexportする形
    - 名前付き関数宣言と同時にexport
    - ```
        export default function sample(props){
            return <div>???</div>
        }
      ```
2. default import (名前なしimport)
    - default exportの内容をそのまま読み込む
    - 

3. 名前付きexport
    - 1ファイルから複数モジュールをexportしたいとき
    - React ではエントリポイントでよく使われます。
    - エントリポイントとは・・・
    - エントリポイントでは別名exportも併用している。（default ???の場合 defaultが読み込まれるのをasで名称を変換）
    - export {default as Title} from "./Title"
    - 1ファイルから複数のモジュールを読み込む
    - import {ccc, sss} from "./index.js"
    - エントリポイントから複数の読み込みをする際に使う。

### Hooksについて
- クラスコンポ―ネントでしか使えなかったことを使えるように
    - コンポーネント内で状態を管理するstate
    - コンポーネントの時間に流れに基づくライフサイクル
- Hooksにより関数コンポーネントを使えるように

- Reactコンポーネント内の値を書き換えたい
    - コンポーネント内の要素をDOMで直接書き換える（従来のjs)
    - 新しい値を使って再描画(再レンダリング)させる。
- Reactコンポーネントが再描画されるきっかけ
    - state 変更時
    - props変更時

1. useStateによるstateの宣言
    - const [state, setState] = useState(initialState)
    - 現在・更新関数・初期値の順

2. stateの更新
    - setState(newState);

3. 具体例
    - const [message, setMessage] = useState('Samples')
    - const [likes, setLikes] = useState(0)
    - const [isShow, setShow] = useStates(false)
    <!-- - setShow(true); -->

- propsとstateの違い
    - propsは親から子に渡されている
    - stateはコンポーネントの中で制御されるような値

- propsへの関数を渡す際の注意
    - NGはonclickメソッドなどに通常()付きで関数を渡したりすると実行されてしまってコールバックでも関数自体でもないので無限レンダリングが発生してしまうことがある。
    - propsに渡すときには関数は実行しない。
