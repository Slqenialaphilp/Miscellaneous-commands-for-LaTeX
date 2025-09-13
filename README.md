# Miscellaneous-commands-for-LaTeX
LaTeX用に定義した雑多なコマンドを提供します。  
主にLuaLaTeX + unicode-mathでの使用を想定しています。それ以外の環境での動作は保証しませんが、特に下でLuaLaTeX専用であると書いたもの以外はおそらく問題なく動くと思われます。  
時折破壊的更新を行います。リポジトリ作成時点では破壊的変更のあるコミットにはそれを明記するつもりですが、忘れる可能性があります。  
CC0です。ご自由にお使いください。Issueなども歓迎します。

## ファイル・コマンド一覧
コマンドの引数は`<意味>`で表します。特記のない限り括弧の種類と引数の扱いは慣習に従います。

### FibBdl.tex
**LuaLaTeXでのみ利用可能です。**  
```\FibBdl[<length*>]{<structure group>, <fiber>; <projection>, <total space>, <base space>}```  
`<length>`は`short` / `long` （デフォルト） / `<dimension>`のいずれかに対応しています。いつかは`min`で`p: E-->>B`の形になるようにしたいとは思っています。  
ファイバー束用のコマンドです。引数を省略する場合にはカンマとセミコロンを適宜省略してください。これらは内部で引数を区切るのに使われているので、必要に応じて引数を波括弧で囲ってください。  
使用例：  
<img width="1498" height="710" alt="スクリーンショット 2025-09-13 025405" src="https://github.com/user-attachments/assets/1c092383-63c4-40e6-97c5-58144fdbe4d5" />

### unimath-utility.tex
`unicode-math`用の便利かもしれないコマンドをまとめています。  
```\DeclareUnimathAlias{<alias>}{original}```  
`unicode-math`では`\begin{document}`へのフックで数学記号のコマンドが定義されるので、単にプリアンブルで`\NewDocumentCopy`を使うとエラーを吐きます。それを防ぐためだけの1行コマンドです。  
  
```\ncm_generate_long_variant:Nnn <cs> {<math class>} {<code point>}```
長い矢印などを定義するときに使います。New Computer Modern用に作ったので名前空間が`ncm`だったり長さが1.484emでハードコードだったりしますが、それはともかく`\ncm_generate_long_variant:Nnn \longtwoheadrightarrow {rel} {"21A0}`のように使います。
