<script lang="ts"></script>
<template>
  <div>
    <h1>関数とオブジェクト page</h1>
    <h2>関数</h2>
    <p>引数が未定義の場合の挙動</p>
    <pre>
      function fn(a, b){
        console.log(a,b)
      }
      fn(1) //引数a: 1, 引数b:undefined
      fn(null,1) //引数a: null, 引数b:1
      fn(1, null) //引数a: 1, 引数b:null
    </pre>
    <p>関数名が重複している場合は、後から宣言した関数が有効</p>
    <p>引数は、argumentsオブジェクトに格納されている</p>
    <pre>
      function fn(){
        console.log(arguments) 
      }
      fn(1,2) // arguments[0]にaが、arguments[1]にbが格納されて出力される

      function fn(){
        console.log(arguments) 
      }
      fn(1,2) // arguments[0]にaが、arguments[1]にbが格納されて出力される

      // 引数が何個入ってくるかわからない場合に使用することがあったが、ES6からは残余引数が使われることが多い
      function func1(...args){
        console.log(args)
      }
      fn(1,2) // [1,2] argumentsとは違い、配列に格納
    </pre>
    <p>returnを定義しない場合はundefinedが返却される</p>

    <h2>関数とオブジェクト</h2>
    <p>関数は「実行可能なオブジェクト」</p>
    <pre>
      function fn(){
        console.log("Hello")
      }
      fn.prop = "World"
      fn.method = function(){
        console.log("Hello World")
      }

      fn() // Hello
      console.log(fn.prop) // World
      fn.method() // Hello World
    </pre>

    <h2>コールバック関数</h2>
    <p>他の関数に引数に対して渡される関数</p>
    <pre>
      function hello(){
        console.log(Hello)
      }
      function fn(cb){
        cb() //コールバック関数を実行
      }

      fn(hello) //fn関数にhello関数(object)を渡す

    </pre>
    <p>特定の振る舞いをする関数を作っておき、渡された関数をその振る舞いと共に実行することができるため、コードの再利用性が高まる</p>
  
    <h2>this</h2>
    <p>「呼び出し元」のオブジェクトへの参照を保持する</p>
    <p>実行コンテキストによってthisの参照先は変わる</p>
    <p>オブジェクトのメソッドとして実行：thisは、呼び出し元のオブジェクト</p>
    <p>関数として実行：thisは、グローバルオブジェクト（windowなど）</p>
    <p>※アロー関数は例外で、メソッドであっても関数扱い</p>
    <pre>
      const obj = {
        name: "Tom",
        hello: function() {
          console.log("hello" + this.name)
        }
      }

      obj.hello() // this = obj のため、"hello Tom"
      const ref = obj.hello;
      ref() // this = global object のため、"Hello"
      window.name = "Mike"
      ref() // this = global object のため、"Hello Mike"
    </pre>

    <p>コールバック関数の場合、引数として「関数」が渡されるため、thisはグローバルオブジェクトとなる</p>
    <pre>
      function fn(cb){
        cb() // objのメソッドではなく、callback関数として渡された関数を実行しているという扱い
      }
      fn(obj.hello) // this = global object
    </pre>

    <p>bind と this</p>
    <p>this や 引数を固定した新しい関数を作成する</p>
    <p>使用時点で関数の実行はしない</p>
    <pre>
      function fn(msg) {
        name: "Tom "
        console.log(this.name + msg)
      }

      const bindFn = fn.bind("Mike", {msg: "Hello"}) // bind(固定するthis, 固定する引数)

      bindFn("Hi") // Mike Hello

      // Tom Hi にならないのが重要ポイント

    </pre>
    <h1>call, apply と this</h1>
    <p>this や 引数 を固定した新しい関数を作成・実行する</p>
    <p>使用時点で関数の実行をする</p>

    <p>apply(thisの参照先obj, 引数に展開する配列)</p>
    <p>call(thisの参照先obj, 引数に渡す値1,引数に渡す値2...)</p>
    <p>複数の引数を受け取る関数に対して配列のデータを渡したい時にapplyがよく使われていたが、ES6からはスプレッド演算子が使用されている</p>
    <pre>
      const arr = [1,2,3,4,5]
      const result = Math.max.apply(null, arr) // apply
      const result = Math.max(...arr) // スプレッド演算子
    </pre>

    <h2>アロー関数</h2>
    <p>ES6から導入された、無名関数の省略記法</p>
    <pre>
      function fn(name){
        return "hello" + name
      }

      const a = function(name){
        return "Hello" + name
      }

      // アロー関数
      const a = (name) => {
        return "Hello" + name
      }

      // アロー関数（引数が一つであれば（）を省略可能）
      const a = name => {
        return "Hello" + name
      }

      // アロー関数（関数内の処理がreturn文だけであればreturnと{}を省略可能）
      const a = name => "Hello" + name

    </pre>

    <table>
      <thead>
      <tr>
        <th>#</th>
        <th>無名関数</th>
        <th>アロー関数</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>this</td>
        <td>⚫︎</td>
        <td>×</td>
      </tr>
      <tr>
        <td>arguments</td>
        <td>⚫︎</td>
        <td>×</td>
      </tr>
      <tr>
        <td>new</td>
        <td>⚫︎</td>
        <td>×</td>
      </tr>
      <tr>
        <td>prototype</td>
        <td>⚫︎</td>
        <td>×</td>
      </tr>
    </tbody>
    </table>

    <p>アロー関数の this の例</p>
    <pre>
      const person = {
        name: 'Tom',
        hello: function(){
          console.log("Hello" + this.name)
        },
        bye(){
          console.log("Bye" + this.name) // 無名関数の省略記法
        },
        sorry: () => {
          console.log("Sorry" + this.name) // アロー関数
        }
      }

      person.hello() // Hello Tom
      person.bye() // bye Tom
      person.sorry() // sorry
      // アロー関数で定義したメソッドのthisは解決されず、グローバルオブジェクトのnameを参照

    </pre>

    <h2>コンストラクタ関数</h2>
    <p>新しくオブジェクトを作成するための雛形となる関数</p>
    <p>コンストラクタ関数を呼び出す際は、new演算子を使用する</p>
    <p>newでオブジェクトを生成することを、インスタンス化という</p>
    <p>newで作成したオブジェクトをインスタンスという</p>
    <pre>
      //慣例で先頭は大文字
      function Person(name,age) {
        this.name = name;
        this.age = age;
      }
      const bob = new Person('Bob', 18)
      const tom = new Person('Tom', 33)
      const sun = new Person('Sun', 33)
    </pre>

    <h2>prototype</h2>
    <p>オブジェクトに存在する特別なプロパティ</p>
    <p>コンストラクタ関数と合わせて使う</p>
    <p>インスタンス化の際に、prototypeへの参照が、作成したインスタンスの__proto__にコピーされる</p>
    <pre>
      //慣例で先頭は大文字
      function Person(name,age) {
        this.name = name;
        this.age = age;
      }

      Person.prototype.hello = function() {
        console.log('hello' + this.name)
      }

      const bob = new Person('Bob', 18)
      const tom = new Person('Tom', 33)
      const sun = new Person('Sun', 33)

      bob.hello(); // hello bob
      tom.hello(); // hello.tom
    </pre>

    <p>以下でも同じように動作するが、メモリ効率の観点から、prototypeを使用することが推奨される</p>
    <pre>
      function Person(name,age) {
        this.name = name;
        this.age = age;
        this.hello = function() {
          console.log('hello' + this.name)
        }
      }
      // この場合、すべてのインスタンスにhello関数のメモリ領域が確保される
      // prototypeへの追加の場合は、確保されるhello関数のメモリ領域は1つで、
      //すべてのインスタンスは__proto__にprototypeへの参照を持っているため、メモリ効率が良い

      const bob = new Person('Bob', 18)
      const tom = new Person('Tom', 33)
      const sun = new Person('Sun', 33)

      bob.hello(); // hello bob
      tom.hello(); // hello.tom
    </pre>
    <h2>new演算子</h2>
    <p>コンストラクター関数からインスタンスを生成するために使用する演算子</p>
    <p>・コンストラクター関数の戻り値がオブジェクトの場合は、空のオブジェクトを返却</p>
    <p>・コンストラクター関数の戻り値がオブジェクト以外の場合は、thisを返却</p>
    <pre>
      // newを疑似的に模した実装

      // コンストラクタ関数
      function fn(a,b) {
        this.a = a;
        this.b = b;
      }
      fn.prototype.c = function() {}

      // newを疑似的に模した実装
      function newOpe(C, ...args) {
        const _this = Object.create(C.prototype); //まずprototypeをコピーし空のオブジェクトを生成
        const result = C.apply(_this, args); // 空のオブジェクトをコンストラクタ関数のthisとして渡す

        if(typeof result === "object" && result !== null) {
          return result
        }
        return _this;
      }

      const instance = newOpe(F,1,2);
    </pre>
    <h2>instanceof</h2>
    <p>どのコンストラクタから生成されたオブジェクトかを確認する</p>
    <p>内部的には、instanceの__proto__と、ターゲットとなるオブジェクトのprototypeの参照先が同じかを確認している</p>
    <p> target instanceof constructor</p>
    <h2>関数コンストラクター</h2>
    <p>関数は実行可能なオブジェクト</p>
    <p>一般的には使用しない</p>
    <pre>

      // 関数コンストラクターから生成したfn1関数 (=オブジェクト)
      const fn1 = new Function('a','b','return a + b')

      // 関数宣言
      function fn2(a,b) {
        return a + b
      }

      fn1(1,2) // 3
      fn2(1,2) // 3
      console.log(fn2 instanceof Function) // true
    </pre>

    <h2>プロトタイプチェーン</h2>
    <p>プロトタイプの多重形成</p>
    <p>階層が浅いものから探しに行く</p>
    <p>OwnProperty ⇒ __proto__ ⇒ __proto__ ... ⇒ Undefined</p>
    <pre>
      function Person(name, age) {
        this.name = name;
        this.age = age;
        this.hello = function() {
          console.log('OwnProperty: hello ' + this.name);
        } 
      }

      // Personオブジェクトのprototype
      Person.prototype.hello = function() {
        console.log('Person: hello ' + this.name);
      }

      // Object の prototype
      Object.prototype./hello = function() {
        console.log('Object: hello ' + this.name);
      }

      const bob = new Person('Bob', 18);
      bob.hello();
    </pre>
    <h2>hasOwnPropterty / in</h2>
    <p>hasOwnProperty : 自分自身のオブジェクトのプロパティに存在するか</p>
    <pre> obj.hasOwnPropety('search condition') // true/false </pre>
    <p>in : プロトタイプチェーンをさかのぼって存在確認</p>
    <pre> console.log('search condition' in obj)</pre>
    <h2>プロトタイプ継承</h2>
    <p>別のコンストラクター関数のプロトタイプを受け継いで、機能を流用できること</p>
    <p>継承：別のコンストラクター関数を受け継ぐこと</p>
    <pre>
      function Person(name, age) {
        this.name = name,
        this.age = age
      }

      Person.prototype.hello = function() {
        console.log('hello', + this.name);
      }

      function Japanese(name, age, gender) {
        Person.call(this, name, age)
      }

      // プロトタイプ継承 (空のオブジェクトに__proto__を持つオブジェクトを生成/代入)
      Japanese.prototype = Object.create(Person.prototype)
      
      // 上書きも可能
      Japanese.prototype.hello = function() {
        console.log('こんにちは', + this.name);
      }
      Japanese.prototype.bye = function() {
        console.log('さようなら', + this.name);
      }

      const taro = new Japanese('Taro', 23, 'Male');
      console.log(taro)
      taro.hello();
    </pre>

    <h2>クラス</h2>
    <p>コンストラクター関数のシンタックスシュガー</p>
    <p>内部的にはコンストラクター関数が実行されている</p>
    <p>クラス継承：ほかのクラスのプロパティとメソッドを継承すること</p>
    <pre>
      class Person {
        constructor(name, age) {
          this.name = name
          this.age = age;
        }

        hello() {
          console.log('hello ' + this.name)
        }
      }

      class Japanese extends Person {
        constructor(name, age, gender) {
          super(name,age)
          this.gender = gender
        }

        hello() {
          console.log('こんにちは ' + this.name)
        }
        bye() {
          console.log('さようなら ' + this.name)
        }
      }

      const bob = new Person('Bob', 23)
      const taro = new Japanese('Taro', 23, 'Male');
      console.log(bob);
      console.log(taro);
    </pre>
    <h2>super</h2>
    <p>継承元の関数を呼び出すためのキーワード</p>
    <p>クラスの中でのみ使用</p>
    <h2>ビルトインオブジェクト</h2>
    <p>コード実行前にJavaScriptエンジンによって自動的に生成されるオブジェクト</p>
    <h2>ラッパーオブジェクト</h2>
    <p>プリミティブ値を内包するオブジェクト</p>
    <pre>
      const a = new String('hello') // const a = 'hello' でも同じ挙動（暗黙的にラッパーオブジェクトが呼ばれている）
      console.log(a);
      console.log(a.toUpperCase);

      const b = new Number(100);
      console.log(b)
      console.log(b.toExponential)
    </pre>
    <h2>Symbol</h2>
    <p>propertyの重複を避けるために、必ず一意の値を返す関数</p>
    <p>ECMAScriptのバージョンが上がる際の競合を避けるために導入された経緯</p>
    <pre>
      const s = Symbol(hello); // new演算子は不要
      console.log(s) // symbol(hello)
      const s2 = Symbol(hello);
      console.log(s === s2) // false

    </pre>
    <h2>プロパティとディスクリプタ</h2>
    <p>プロパティに設定できるもの</p>
    <li>value: 値</li>
    <li>configurable: 設定変更可能性</li>
    <li>enumerable: 列挙可能性</li>
    <li>wraitable: 値の変更可能性</li>
    <li>set: </li>
    <li>get: </li>
    <pre>
      const obj = {prop: 0};
      const descriptor = Object.getOwnPropertyDescriptor(obj, prop)
      console.log(descriptor)

      const obj2 = {};
      Object.defineProperty(obj, 'prop', {
        value: 0
      })
      const descriptor2 = Object.getOwnPropertyDescriptor(obj, prop)
      console.log(descriptor2)
    </pre>
    <pre>
      class Person {
        constructor(name, age) {
          this.‗name = name,
          this._age = age
        }

        get: name() {
          return this._name
        }

        set: name(val) {
          this._name = vali;
        }

        static hello() {
          console.log('hello') // staticメソッド
        }
      }

      Person.hello(); // インスタンス化せずにコールできる
    </pre>
  </div>
</template>
