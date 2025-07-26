# Vim学習ゲーム 開発ガイド

## 1. 開発環境の準備

### 1.1 必要なツールの確認
このプロジェクトでは以下のツールを使用します：

- **Node.js** (バージョン14以上)
- **npm** (Node.jsに同梱されています)
- **React** (バージョン18以上)
- **Visual Studio Code** (推奨エディタ)

### 1.2 Node.jsとnpmのインストール確認
ターミナルで以下のコマンドを実行して、インストールされているバージョンを確認します：

```bash
node -v
npm -v
```

Node.jsがインストールされていない場合は、以下の手順でインストールします：
1. https://nodejs.org/ にアクセス
2. LTSバージョンをダウンロードしてインストール

### 1.3 Reactプロジェクトの作成
以下のコマンドで新しいReactプロジェクトを作成します：

```bash
npx create-react-app vim-learning-game
cd vim-learning-game
```

### 1.4 開発サーバーの起動
以下のコマンドで開発サーバーを起動します：

```bash
npm start
```

ブラウザで http://localhost:3000 にアクセスすると、Reactの初期画面が表示されます。

## 2. プロジェクト構造の理解

### 2.1 基本的なディレクトリ構造
```
vim-learning-game/
├── node_modules/
├── public/
│   ├── index.html
│   └── ...
├── src/
│   ├── App.js
│   ├── App.css
│   ├── index.js
│   └── ...
├── package.json
└── ...
```

### 2.2 重要なファイルの説明
- **src/index.js**: アプリケーションのエントリーポイント
- **src/App.js**: メインのアプリケーションコンポーネント
- **public/index.html**: ルートHTMLファイル

### 2.3 コンポーネントの配置
コンポーネントは`src/components/`ディレクトリを作成してその中に配置します：

```
src/
├── components/
│   ├── Header.js
│   ├── MainMenu.js
│   └── ...
├── App.js
└── index.js
```

## 3. 最初のコンポーネント作成

### 3.1 関数コンポーネントの基本構造
Reactの関数コンポーネントは以下のようになります：

```jsx
// src/components/Header.js
import React from 'react';

const Header = () => {
  return (
    <header>
      <h1>Vim学習ゲーム</h1>
    </header>
  );
};

export default Header;
```

### 3.2 JSXの基本
JSXはJavaScriptの拡張構文で、HTMLのような構文でUIを記述できます：

```jsx
const element = (
  <div>
    <h1>Hello, world!</h1>
    <p>これはJSXの例です</p>
  </div>
);
```

### 3.3 コンポーネントのインポート/エクスポート
コンポーネントを使用するには、他のファイルからインポートする必要があります：

```jsx
// App.jsでHeaderコンポーネントを使用する場合
import Header from './components/Header';

function App() {
  return (
    <div className="App">
      <Header />
    </div>
  );
}
```

## 4. スタイリングの方法

### 4.1 CSSファイルの作成
コンポーネントごとにCSSファイルを作成できます：

```css
/* src/components/Header.css */
.header {
  background-color: #1E1E1E;
  color: #4CAF50;
  padding: 1rem;
  text-align: center;
}
```

### 4.2 CSSのインポート
コンポーネントファイルでCSSをインポートします：

```jsx
// src/components/Header.js
import React from 'react';
import './Header.css';

const Header = () => {
  return (
    <header className="header">
      <h1>Vim学習ゲーム</h1>
    </header>
  );
};

export default Header;
```

## 5. 状態管理の基本

### 5.1 useStateフックの使い方
コンポーネント内で状態を管理するにはuseStateフックを使用します：

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>カウント: {count}</p>
      <button onClick={handleClick}>クリック</button>
    </div>
  );
};

export default Counter;
```

### 5.2 イベントハンドリング
ユーザーの操作に応じて処理を行うには、イベントハンドラを設定します：

```jsx
const Button = () => {
  const handleClick = () => {
    alert('ボタンがクリックされました！');
  };

  return (
    <button onClick={handleClick}>
      クリックしてください
    </button>
  );
};
```

## 6. コンポーネント実装手順

### 6.1 各コンポーネントの実装ステップ
各コンポーネントは以下の手順で実装します：

1. **コンポーネントファイルの作成**
   - `src/components/`ディレクトリに新しいコンポーネントファイルを作成

2. **基本的な構造の実装**
   - 関数コンポーネントの基本構造を作成
   - 必要なHTML構造をJSXで記述

3. **スタイリングの追加**
   - CSSファイルを作成してスタイルを定義
   - コンポーネントにクラス名を適用

4. **状態管理の追加（必要な場合）**
   - useStateフックを使用して状態を管理
   - イベントハンドラを実装

5. **親コンポーネントでの使用**
   - 親コンポーネントで新規コンポーネントをインポート
   - JSX内でコンポーネントを使用

6. **ブラウザでの確認**
   - 開発サーバーで変更を確認
   - 必要に応じて調整

### 6.2 実装例：Buttonコンポーネント
```jsx
// src/components/Button.js
import React from 'react';
import './Button.css';

const Button = ({ label, onClick, variant = 'primary', disabled = false }) => {
  return (
    <button 
      className={`button button-${variant}`}
      onClick={onClick}
      disabled={disabled}
    >
      {label}
    </button>
  );
};

export default Button;
```

```css
/* src/components/Button.css */
.button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.2s ease;
}

.button-primary {
  background-color: #4CAF50;
  color: white;
}

.button-primary:hover:not(:disabled) {
  background-color: #45a049;
  transform: translateY(-2px);
}

.button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}
```

このガイドに従って、1つずつコンポーネントを実装していきましょう。各コンポーネント実装後、ブラウザで表示を確認しながら開発を進めることができます。
