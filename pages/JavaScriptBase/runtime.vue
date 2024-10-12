<script lang="ts"></script>
<template>
  <div>
    <h1>実行環境 page</h1>
    <!-- <DesignPatternAdapter /> -->
    <p></p>
    <h2>実行コンテキスト</h2>
    <ul>
      <li>グローバルコンテキスト</li>
      <ul>
        <li>実行中のコンテキスト内の変数、関数</li>
        <li>グローバルオブジェクト</li>
        <li>this</li>
      </ul>
      <li>関数コンテキスト</li>
      <ul>
        <li>実行中のコンテキスト内の変数、関数</li>
        <li>argument</li>
        <li>super</li>
        <li>this</li>
        <li>外部変数（関数ブロック外）</li>
      </ul>
      <li>evalコンテキスト</li>
    </ul>
    <h2>コールスタック</h2>
    <p>実行中のコードが辿ってきたコンテキストのスタック</p>
    <p>必ず最下層はグローバルオブジェクト</p>
    <p></p>
    <h2>Hoisting（宣言の巻き上げ）</h2>
    <p>コンテキスト内で宣言した関数や変数の定義を、「コード実行前」にメモリに配置すること</p>
    <p>コンテキストの生成時に必ず実施される</p>
    <li>let,const: メモリ確保はするが初期化はしない → 初期化前のアクセスはエラー</li>
    <li>var,: メモリ確保と初期化をする → 初期化前のアクセスはundefined</li>
    <p>通常の関数宣言の場合は初期化されるのでエラーにならないが、関数式（無名関数）の場合は変数扱いのため未定義</p>
    <p>例</p>
    <pre>
      
      //no error
      a()
      function a() {
        console.log('a is called')
      }

      //error
      b()
      const b = function() {
        console.log('b is called')
      }
    </pre>
</div>
</template>
