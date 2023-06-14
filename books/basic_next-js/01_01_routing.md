---
title: "RoutingとURLを受け取る方法"
---

### Pages Router

pages ディレクトリにディレクトリを作成することでルーティングを作成する
ファイルをページとして認識する

----
### App Router

app ディレクトリにディレクトリを作成することでルーティングを作成する
src/app ディレクトリ配下の「page.tsx」をページとして認識する

----
### Route Group

ルーティングのパスに影響を与えないディレクトリを作成する方法の一つ
ディレクトリを()で囲む必要がある。
例）　(example)ディレクトリ

----
### Dynamic Routes と URLを受け取る方法

##### シンプルな形

動的なルーティングを可能にする
\[]でディレクトリ名を囲む

例）app/blog/\[id]というディレクトリ構成で考える
「なんとかcom/blog/hoge1」にアクセスした場合、hoge1を受け取るには
\[id]配下のpage.tsxを以下のようにする

``` TypeScript
const Page = ({params}:{params: {id:string[]}}) => {
    return <div>Blog ID:{params.id}</div>;
};

export default Page;
```

paramsという配列のidキーに対応する値を表示するって感じの理解でいいのだと思う

URL：なんとかcom/blog/hoge1/hoge2の場合は、
\[...id]とすることで配列の形で受け取ることができるっぽい

##### catch-all-segments の設定

app/blog/\[id]/\[userId]/\[categoryId]　は、どうするのって話

このディレクトリ構成で「なんとかcom/1/2/3」にアクセスした場合、
```{ id: '1', userId: '2', categoryId: '3' }```という配列が得られるっぽい

\[categoryId]配下に、以下の内容のpage.tsxを配置して、それぞれの値を受け取ることができる。

```ts
const Page = ({
    params,
  }: {
    params: { id: string, userId: string, categoryId: string },
  }) => {
    console.log(params);
    return <div className="m-4 font-bold">Blog ID:{params.id},User ID:{params.userId},Category ID:{params.categoryId} </div>;
  };
  
  export default Page;
```

\[userID] 配下にも別の page.tsx を配置して別の画面表示ってこともできる。
ユーザーの投稿一覧ページだとかさ
