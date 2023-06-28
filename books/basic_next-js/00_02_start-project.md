---
title: "プロジェクトを作成する"
---

# インストール

# 開発開始

```shell
npx create-next-app@latest
```

# 個人的な処理

個人的に、デフォルトの globals.css が好きではないので以下のように変更を行う。

変更点は、下のbody要素の削除。

```diff css:src/app/global.css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --foreground-rgb: 0, 0, 0;
  --background-start-rgb: 214, 219, 220;
  --background-end-rgb: 255, 255, 255;
}

@media (prefers-color-scheme: dark) {
  :root {
    --foreground-rgb: 255, 255, 255;
    --background-start-rgb: 0, 0, 0;
    --background-end-rgb: 0, 0, 0;
  }
}

- body {
-   color: rgb(var(--foreground-rgb));
-   background: linear-gradient(
-       to bottom,
-       transparent,
-       rgb(var(--background-end-rgb))
-     )
-     rgb(var(--background-start-rgb));
}
```

