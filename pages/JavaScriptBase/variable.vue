<script lang="ts"></script>
<template>
  <div>
    <h1>変数 page</h1>

    <h2>let, const, var</h2>
    <table>
      <thead>
        <tr>
          <th>タイプ</th>
          <th>再宣言</th>
          <th>再代入</th>
          <th>スコープ</th>
          <th>初期化</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>let</td>
          <td>×</td>
          <td>⚫︎</td>
          <td>ブロック</td>
          <td>×</td>
        </tr>
        <tr>
          <td>const</td>
          <td>×</td>
          <td>×</td>
          <td>ブロック</td>
          <td>×</td>
        </tr>
        <tr>
          <td>var</td>
          <td>⚫︎</td>
          <td>⚫︎</td>
          <td>関数</td>
          <td>undefined</td>
        </tr>
      </tbody>
    </table>
    <h2>データ型</h2>
    <h2>型変換</h2>
    <p>動的型付け言語</p>
    <p>静的型付け言語</p>
    <h2>厳格な等価性と抽象的な等価性</h2>
    <p>=== : 型も含めて比較</p>
    <p>== : 型は比較しない</p>
    <h2>truthy / falsy</h2>
    <p>falsy: false, 0, 0n, "", NaN, undefined, null</p>
    <p>truthy: 上記以外全て</p>
    <p>if文の条件でよく使う</p>
    <h2>AND / OR</h2>
    <h3>AND(&&)</h3>
    <p>与えられた値のうち、左からスタートして、最初にfalsyだった値を返却する</p>
    <p>全てがtruthyだった場合は、最右の値を返却する</p>
    <pre>
      
      1 && 2 && 3 // 3
      0 && 2 && 3 // 0
      0 && 0 // 0
      "" && "Tom" // ""
      "Tom" && func() // func() 
    </pre>
    <h3>OR(||)</h3>
    <p>与えられた式のうち、左からスタートして、最初にtruthyだった値を返却する</p>
    <p>全てがfalsyだった場合は、最右の値を返却する</p>
    <pre>

      1 || 2 || 3 // 1
      0 || 2 || 3 // 2
      0 || 0 // 0
      "" || "Tom" // "Tom"
      "Tom" || func() // "Tom"
    </pre>
    <h2>プリミティブ型とオブジェクト</h2>
    <h3>プリミティブ型</h3>
    <p>String,Number,Boolean, Undefined, Null, Symbol, BigInt</p>
    <p>変数には「値」が格納される</p>
    <p>immutable (一度作成されると、その値を変更できない)</p>
    <pre>

      let a = "Hello" // メモリ上に "Hello" を格納 + そこへのアドレスを持つaを格納
      a = "Bye" // メモリ上に "Bye" を格納 + a の参照先アドレスを変更

      // ★ メモリ上、"Hello" と "Bye" は異なるアドレス → immutableである
    </pre>
    <h3>オブジェクト: Object(それ以外)</h3>
    <p>変数には「参照」が格納される</p>
    <p>mutable</p>
    <p>オブジェクトは、参照を名前付き（key/prop）で管理する入れ物</p>
    <pre>

      let obj = {  // objにはオブジェクト{...}への参照が格納
        a: "Hello" // a には、"Hello" への参照が格納
      }

      // obj → {...} → a → "Hello

    </pre>
    <h2>参照とコピー</h2>
    <p>プリミティブ型のコピー：参照先の「値」がコピーされる</p>
    <p>オブジェクトのコピー：オブジェクトへの「参照」がコピーされる</p>

    <h2>参照とconst</h2>
    <p>constがロックするものは変数の「値」</p>
    <p>プリミティブ型：再代入は不可能。（値が変更されるため）</p>
    <p>オブジェクト：再代入は不可能。（値が変更されるため）。ただ、値（参照先）が変わらないため、オブジェクトの中身の変更は可能</p>

    <h2>参照と引数</h2>
    <p>関数の引数がプリミティブ型かオブジェクトかによって挙動に違いがある</p>
    <pre>

      // プリミティブ型
      let a = 0
      function fn(arg) {
        arg1 = 1
        console.log(a, arg)
      }
      fn(a) // 0 1

      // オブジェクト
      // 引数(arg)に渡した値はオブジェクト(a)への参照先のため、関数内での変更は変数aの参照先のオブジェクトにも影響する
      let a = {
        prop: 0
      }
      function fn(arg) {
        arg.prop = 1
        console.log(b, arg)
      }
      fn(a) // {prop: 1} {prop: 1}

      // 以下の関数であれば、別のオブジェクトが生成される
      function fn(arg) {
        arg = {prop: 1}
        console.log(b, arg)
      }
      fn(a) // {prop: 0} {prop: 1}
    </pre>

    <h2>参照と分割代入</h2>
    <p>分割代入：オブジェクトから特定のプロパティを抽出して宣言を行う</p>

    <pre>

      //パターン①（通常の分割代入）
      const a = { prop: 0}
      let { prop } = a;
      prop = 1
      console.log(a, prop) // {prop: 0} 1


      // パターン②（引数で受け取ったオブジェクトを関数内で分割代入）
      const a = { prop: 0}
      function fn(obj) {
        let {prop} = obj
        prop = 1
        console.log(a, prop) 
      }

      fn(a) // {prop: 0} 1

      // パターン③（パターン②の簡略版。引数の時点で分割代入する（
      const a = { prop: 0}
      function fn({ prop }) {
        prop = 1
        console.log(a, prop) 
      }

      fn(a) // {prop: 0} 1
      
      // パターン④ （多階層のオブジェクトの場合）
      // ★ prop1.prop2を変更すると、変数aの参照先のオブジェクトのprop2も変更されることが重要
      const a = { 
        prop1: {
          prop2: 0
        } 
      }
      let { prop1 } = a;
      console.log(prop1) // {prop2: 0}
      prop1.prop2 = 1
      console.log(a, prop1) // {prop1: {prop2: 1}} {prop2,1}

    </pre>

    <h2>参照の比較と値の比較</h2>
    <p>変数に何が核のされているかによるため、以下の挙動となる</p>
    <p>プリミティブ型：値の比較</p>
    <p>オブジェクト：参照の比較</p>
    <pre>
      const a = {prop: 0}
      const b = {prop: 0}
      const c = a

      console.log(a === b) // false
      console.log(a == b) // false
      console.log(a.prop === b.prop) // true
      console.log(a === c) // true
    </pre>
  </div>
</template>
