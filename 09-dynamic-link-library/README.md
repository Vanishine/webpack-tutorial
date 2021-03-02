## 为什么要使用 DLL

分割 chunks 效果其实是非常有限的，需要满足以下条件：

- 必须是所有入口的公共库。这意味着必须是来自 `node_modules` 目录，并且当入口变多的时候公用的部分也会变得更少。
- 只能提取到单个文件，无法进行拆分。多个库，例如同时使用 jQuery 和 Lodash，那么他们只能成为一个整体，无法进行细粒度的复用。

而使用 DLL 配合清单可以更加灵活的重组。

如可以将 5 个模块任意组合进行拆分与组合：

```text
AB 如何任何使用 A 都会用到 B 则可以将他们视作一个 DLL
C
DEF
```

每个库可以选择 DLL 进入引入：

```
a: AB DEF
b: AB C
c: C
```