---
title: "Link コンポーネント"
---

# Linkコンポーネントを使用する理由

# 使い方

# prefetch の設定

Linkコンポーネントの機能の一つ。デフォルトでオンになっている。
リンクにカーソルを当てるとリンク先のページに関する JavaScript ファイルなどがバックグランドで自動でダウンロードされる。

```TypeScript:src/app/page.tsx
// Linkコンポーネントをインポート
import Link from 'next/link';

const Page = () => {
  return (
    <div>
      <Link href="/">
        リンクテキスト
      </Link>
      <h1>Home</h1>
    </div>
  );
};

export default Page;
```

