# Miscellaneous-commands-for-LaTeX
LaTeX用に定義した雑多なコマンドを提供します。**多くのコマンドがexpl3を使用しているので、`\ExplSyntaxOn`と`\ExplSyntaxOff`で挟むなど適宜対応してください。**  
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

### unimath-utility.tex, longvariant.tex
`unicode-math`用の便利かもしれないコマンドをまとめています。  
```\DeclareUnimathAlias{<alias>}{original}```  
`unicode-math`では`\begin{document}`へのフックで数学記号のコマンドが定義されるので、単にプリアンブルで`\NewDocumentCopy`を使うとエラーを吐きます。それを防ぐためだけの1行コマンドです。  
  
```\ncm_generate_long_variant:Nnn <cs> {<math class>} {<code point>}```
長い矢印などを定義するときに使います。New Computer Modern用に作ったので名前空間が`ncm`だったり長さが1.484emでハードコードだったりしますが、それはともかく`\ncm_generate_long_variant:Nnn \longtwoheadrightarrow {rel} {"21A0}`のように使います。  
longvariant.texにNew Computer Modernが対応していそうなものを一通り書き並べてあります。

### prooftree.tex
bussproofsパッケージを使った証明木をやや簡単に書けるようにしたコマンドです。  
基礎論の講義のために作って以来長らく使っていないので使い方をよく覚えていないのですが、`\Iniseq`・`\Inf{<0/1/2>}`を駆使していくようです。  
使用例：
```
\begin{prooftree}
	\IniSeq \varphi
	\Inf1[wkL]{\psi,\,\varphi & \varphi}
	\Inf1[exL]{\varphi,\,\psi & \varphi}
	\Inf1[notR]{\psi & \varphi,\,\lnot\varphi}
	\IniSeq \psi
	\Inf1[wkR]{\psi & \psi,\,\varphi}
	\Inf1[exR]{\psi & \varphi,\,\psi}
	\Inf1[notL]{\lnot\psi,\,\psi & \varphi}
	\Inf2[impL]{\psi,\,\psi,\,\lnot\varphi\rightarrow\lnot\psi & \varphi,\,\varphi}
	\Inf1[cntL]{\psi,\,\lnot\varphi\rightarrow\lnot\psi & \varphi,\,\varphi}
	\Inf1[cntR]{\psi,\,\lnot\varphi\rightarrow\lnot\psi & \varphi}
	\Inf1[impR]{\lnot\varphi\rightarrow\lnot\psi & \psi\rightarrow\varphi}
	\Inf1[impR]{& (\lnot\varphi\rightarrow\lnot\psi) \rightarrow (\psi\rightarrow\varphi)}
\end{prooftree}
```

### mathutil
数学用の簡単なコマンドをまとめています。  
`\vvec{<comma separated list>}`
縦ベクトルを書くときに毎度`pmatrix`を書くのは辛いので、`\vvec{x,y,z}`のようにカンマ区切りで変数を入れられるようにしました。カンマは内部で区切り文字として扱われるので、`\FibBdl`同様必要に応じて波括弧で囲ってください。  
  
`\sfrac{<numerator>}{<denominator>}`  
スラッシュの分数です。LuaLaTeXを使っている場合にはプリミティブを、そうでない場合には`xfrac`パッケージを読み込みます。  
`\quot{<numerator>/<denominator>}`  
**分子と分母の間にあるスラッシュは必須です。**（つまり`\quot{X/Y}`のように使います。）  
`\sfrac`とほぼ同様ですが、大きさを少しだけいじってあります。  
<s>usrguide.pdfとか読みまくって何が起きているか理解できる人なら`\quotient`も便利だと思います。</s>