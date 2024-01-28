---
title: "【useFileList】ファイルの一覧を取得するカスタムフック"
---



# カスタムフックのコード

```ts:useFileList.ts
import { FileEntry, readDir } from '@tauri-apps/api/fs';
import { useEffect, useState } from 'react';


const useFileList = (rootPath: string) => {
    const [fileList, setFileList] = useState<FileEntry[]>([]);
    const [loading, setLoading] = useState<boolean>(true);


    useEffect(() => {
        const fetchData = async () => {
            try {
                const result = await readDir(rootPath);
                const sorted = result.slice().sort(
                    (a, b) => a.path.localeCompare(b.path)
                );
                setFileList(sorted);
                setLoading(false);
            } catch (error) {
                console.error('データの取得エラー:', error);
                setLoading(false);
            }
        };
        // fetchData関数を呼び出し
        fetchData();
    }, [rootPath]); // rootPathやoptionsが変更されたときに再実行

    // ファイルエントリとローディング状態を返す
    return { fileList, loading };
};

export default useFileList;
```

# 使い方


```ts
// 保存したファイルからインポート
import useFileList from "../hooks/useFileList"

function Demo({ path }: { path: string }) {
    const { fileList, loading } = useFileList(path)

    if (loading === true) {
        return <p>Loading</p>
    }

    return (
        <>
            <ul>
                {
                    fileList.map((file, index) =>
                        <li key={index}>{file.name}</li>
                    )
                }
            </ul>
        </>
    )
}

export default Demo
```
