# Reactの基本機能解説

## 目次
1. [はじめに](#はじめに)
2. [Hooks](#hooks)
   - [useState](#usestate)
   - [useEffect](#useeffect)
   - [useContext](#usecontext)
   - [useRef](#useref)
   - [useMemo](#usememo)
   - [useCallback](#usecallback)
3. [Suspense](#suspense)
4. [その他のuse関数](#その他のuse関数)
   - [useReducer](#usereducer)
   - [useLayoutEffect](#uselayouteffect)
   - [useImperativeHandle](#useimperativehandle)

## はじめに

Reactは、ユーザーインターフェースを構築するためのJavaScriptライブラリです。本記事では、Reactの基本的な機能、特にHooks、Suspense、およびその他のuse関数について解説します。

## Hooks

Hooksは、React 16.8で導入された機能で、クラスコンポーネントを書かずに状態やその他のReactの機能を使用できるようにします。

### useState

`useState`は、関数コンポーネント内で状態を管理するためのHookです。

```javascript
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>カウント: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        増加
      </button>
    </div>
  );
}
```

### useEffect

`useEffect`は、副作用を実行するためのHookです。コンポーネントのレンダリング後に実行されます。

```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `${count}回クリックされました`;
  }, [count]);

  return (
    <div>
      <p>{count}回クリックされました</p>
      <button onClick={() => setCount(count + 1)}>
        クリック
      </button>
    </div>
  );
}
```

### useContext

`useContext`は、Reactのコンテキストを簡単に使用するためのHookです。

```javascript
import React, { useContext } from 'react';

const ThemeContext = React.createContext('light');

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button style={{ background: theme }}>テーマ付きボタン</button>;
}
```

### useRef

`useRef`は、DOMノードへの参照や、再レンダリングをトリガーせずに値を保持するために使用されます。

```javascript
import React, { useRef } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    inputEl.current.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>入力にフォーカス</button>
    </>
  );
}
```

### useMemo

`useMemo`は、計算コストの高い関数の結果をメモ化するために使用されます。

```javascript
import React, { useMemo } from 'react';

function ExpensiveComponent({ a, b }) {
  const expensiveResult = useMemo(() => {
    // 複雑な計算
    return a * b;
  }, [a, b]);

  return <div>{expensiveResult}</div>;
}
```

### useCallback

`useCallback`は、コールバック関数をメモ化するために使用されます。

```javascript
import React, { useCallback } from 'react';

function ParentComponent() {
  const [count, setCount] = useState(0);

  const incrementCount = useCallback(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return <ChildComponent onIncrement={incrementCount} />;
}
```

## Suspense

Suspenseは、コンポーネントがレンダリングを完了する前に何かを待機できるようにする機能です。

```javascript
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./LazyComponent'));

function MyComponent() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

## その他のuse関数

### useReducer

`useReducer`は、複雑な状態ロジックを管理するためのHookです。

```javascript
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}
```

### useLayoutEffect

`useLayoutEffect`は`useEffect`と似ていますが、DOMの変更後、ブラウザが画面を描画する前に同期的に実行されます。

```javascript
import React, { useLayoutEffect, useRef } from 'react';

function Tooltip() {
  const tooltipRef = useRef();

  useLayoutEffect(() => {
    const { current } = tooltipRef;
    const { width, height } = current.getBoundingClientRect();
    current.style.left = `${window.innerWidth / 2 - width / 2}px`;
    current.style.top = `${window.innerHeight / 2 - height / 2}px`;
  }, []);

  return <div ref={tooltipRef}>これはツールチップです</div>;
}
```

### useImperativeHandle

`useImperativeHandle`は、親コンポーネントに公開するインスタンス値をカスタマイズするために使用されます。

```javascript
import React, { useRef, useImperativeHandle, forwardRef } from 'react';

const ChildComponent = forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));

  return <input ref={inputRef} />;
});

function ParentComponent() {
  const childRef = useRef();

  const handleClick = () => {
    childRef.current.focus();
  };

  return (
    <>
      <ChildComponent ref={childRef} />
      <button onClick={handleClick}>子コンポーネントにフォーカス</button>
    </>
  );
}
```

以上が、Reactの基本的な機能の概要です。これらの機能を理解し適切に使用することで、効率的で再利用可能なReactコンポーネントを作成することができます。
