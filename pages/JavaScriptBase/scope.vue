<script lang="ts"></script>
<template>
  <div>
    <h1>Scope page</h1>
    <h2>スコープ</h2>
    <li>s</li>
    <h2>レキシカルスコープ</h2>
    <p>コードを書く場所によって参照できる変数が変わるスコープ</p>
    <li>実行中のコードから見た外部スコープ</li>
    <li>どのようにしてスコープを決定するかの仕様</li>
    <h2>スコープチェーン</h2>
    <p>変数名が重複するものが他階層に存在する場合は、内側のスコープから順番にグローバルスコープまで探索</p>
    <h2>クロージャー</h2>
    <p>レキシカルスコープの変数を関数が使用している状態</p>
    <p>クロージャーを使用して、独特な機能を持った関数を定義できる</p>
    <h3>プライベート変数の定義</h3>
    <p>以下の例1でも動作は問題ないが、変数numをグローバルに定義しているため、意図しないnumの変更を防げない</p>
    <pre>
      例1
      let num = 0
      function increment() {
          num++
          console.log(num)
      }
      
      inc()
      inc()
    </pre>
    <p>以下の例2では、numの初期化はincrementFactory関数の実行時のみのため、numをプライベート変数として定義できる</p>
      <li>関数スコープ内で宣言しているnumは、increment()で使用する値を関数外部から変更されない</li>
      <li>numの値は毎回のinc()の際に初期化されないため、正しくインクリメントの動作を実現できる</li>
    <pre>

      function incFactory(){
        let num = 0;
        function increment() {
          num++
          console.log(num)
        }
        return increment;
      }

      const inc = incFactory();
      inc()
      inc()
    </pre>
    <h3>動的な関数の生成</h3>
    <p>引数で渡した値を保持したまま、関数を生成できるため、挙動の異なる関数の定義が可能</p>
    <pre>
      function addNumberFactory(num) {
        function addNumber(balue) {
          return num + value
        }
        return addNumber;
      }

      //5を加算する関数を作成
      const add5 = addNumber(5)
      const result = add5(10) // 15

      //10を加算する関数を作成
      const add10 = addNumber(10)
      const result = add5(10) // 20

    </pre>
    <h2>即時関数</h2>
    <p>関数定義と同時に、「一度だけ」実行される関数</p>
    <pre>
      function a() {
        console.log('called')
      }

      (function() {
        console.log('called')
      })()

      // 以下の利用ケースが多い

      let fn = (function() {
        let privateVal = 1
        let publicVal = 2
        function privateFn() {
          console.log('privateFn is called')
        }
        function publicFn() {
          console.log('publicFn is called')
        }

        return {
          publicVal,publicFn
        }
      })

      // 外からは以下のみ使用可能
      fn.publicVal // 1
      fn.publicFn() // publicFn is called
      
    </pre>
  </div>
</template>
