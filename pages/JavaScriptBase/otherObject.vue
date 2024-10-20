<script lang="ts"></script>
<template>
  <div>
    <h1>様々なオブジェクト page</h1>
    <h2>Proxy</h2>
    <p>プロパティの操作に独自の処理を追加するためのオブジェクト</p>
    <pre>
      const targetObj = {a: 0}
      const handler = {
        set: function(target, prop, value, receiver) {
          console.log(`[set]: ${prop}` )
          target[prop] = value;

        }
        get: function(target, prop, receiver) {
          console.log(`[get]: ${prop}` )
          return target[prop]
        }
        deleteProperty: function(target, prop) {
          console.log(`[delete]: ${prop}` )
          return target[prop]
        }
      }

      const pxy = new Proxy(targetObj, handler)
      pxy.a = 1
      pxy.a;
      delete pxy.a
    </pre>
    <p>実用例</p>
    <pre>
      // 値の変更を許可しない
      set function(target, prop, value,receiver){
        throw new Error('cannot add prop.')
      }
      // 存在しないプロパティの場合にエラーを返却
      get: function(target, prop, receiver) {
        if(target.hasOwnProperty(prop)) {
          return target[prop]
        } else {
          return "-1"
        }
      }
    </pre>

    <h2>Reflect</h2>
    <p>JSエンジンの内部の汎用的な関数を呼び出すメソッドが格納されているオブジェクト</p>
    <p>①内部メソッドを呼び出す関数の格納場所</p>
    <p>②Proxyと合わせて使用するため</p>
    <pre>
      class C {
        constructor(a,b) {
          this.a = a;
          this.b = b;
        }
      }
      const obj1 = new C(1,2)
      console.log(obj1)
      // 演算子表記（new）だったものを、関数表記できる
      //コールバック関数の引数に渡したい時など、、
      const obj2 = Reflect.construct(C, [1,2]);
      console.log(obj2)

      console.log('c' in obj1);
      console.log(Reflect.has(obj1, 'c'))

      // ObjectのdefinePropertyは、trycatchで記載が必要
      try {
        Object.defineProperty
      } catch (e){

      }

      // Reflectの場合は、true/falseが返却される
      if(Reflect.defineProperty) {

      } else {

      }

      //
    </pre>
    <h2>Reflect と Proxy</h2>
    <pre>
      const targetObj = {a: 0}
      const handler = {
        get: function(target, prop, receiver) {
            if(target.hasOwnProperty(prop)) {
            return target[prop]
          } else {
            return "-1"
          }
        }
      }

      const pxy = new Proxy(targetObj, handler)
      console.log(pxy.b)   
      
      const targetObj = {
        a: 0,
        get value() {
          return this.b
        }
      }
      const handler = {
        get: function(target, prop, receiver) {
            console.log(receiver)
            if(target.hasOwnProperty(prop)) {
            return Reflect.get(target, prop, receiver)
          } else {
            return "-1"
          }
        }
      }

      const pxy = new Proxy(targetObj, handler)
      console.log(pxy.a)    
      console.log(pxy.value)    
      console.log(pxy.b)    
    </pre>

    <h2>WeakMap</h2>
    <p>弱い参照でオブジェクトを保持するコレクション</p>
    <p>キーは必ずオブジェクト</p>
    <p>for...of のような反復処理は使用できない（Mapでは使用できるが）</p>
    <pre>

      const wm = new WeakMap();
      
      let obj = {};
      wm.set(obj, 'value1');
      
      obj = null
      // この時点で、objへの参照が切れてしまう
      // weakMapでは、objをキーとしているmapについて、ガベージコレクションする

      console.log(wm.get(obj))
      console.log(wm.has(obj))
      console.log(wm.delete(obj))
    </pre>

    <h2>WeakMapとプライベート変数</h2>
    <p>今？は普通にclassでプライベート変数が宣言できるから不要な構文かも</p>
    <pre>
      const wm = new WeakMap()

      export class Person {
        constructor(name) {
          wm.set(this, {
            name
          })
        }
        hello() {
          console.log(`hello ${wm.get(this.name)}`)
        }
      }

      import { Person } from ...;
      const tim = new Person('Tim')
      tim.hello();
    </pre>
    <h2>JSON</h2>
    <p>JSON.parse: JSON → Object</p>
    <p>JSON.stringify: Object → JSON</p>
    <pre>
      const obj = {a:b, b: 1, c: 2};
      const json = JSON.stringify(obj)
      console.log(json)
      console.log(typeOf json)

      function replacer(prop,value){
        if(value < 1) {
          return;
        } 
        return value
      }
      const json2 = JSON.stringify(obj, replacer)
      console.log(json2)

      const obj3 = JSON.parse(json)
      console.log(obj3)
    </pre>
    <h2>Storage</h2>
    <p>ブラウザの保存領域にデータを格納するためのオブジェクト</p>
    <p>localStorage</p>
    <pre>
      localStorage.setItem('key', 'value');
      localStorage.setItem('key2', '1');
      localStorage.setItem('key3', '2');

      const result localStorage.getItem('key')
      console.log(result)
      // localStorageのメソッドは同期処理
      console.log('end')
    </pre>

    <h2>Array</h2>
    <pre>
      const arry = [1,2,3,4,5]
      arry.push(6)
      arry.unShift(6)
      const result1 = arry.pop()
      const result2 = arry.shift()
      const result2 = arry.splice(0,1)
      const result2 = arry.splice(0,3,1,2)
      console.log(arry,result)
      const arry2 = arry.concat([6,7,8])
      const arry3 = [0, ...arry, 6,7,8]
    </pre>
    <pre>
      const arry = [1,2,3,4,5]
      arry.forEach(function(v,i,arry){
        console.log(v)
      })

      const newArry = arry.map(function(v,i,arry){
        console.log(v)
        return v * 2;
      })
      console.log(newArry)

      const filterArry = arry.filter(function(v,i,arry) {
        return i >= 1;
      })
      
      const result = arry.reduce(function(accu, curr) {
        console.log(accu,curr)
        return accu + curr
      })
    </pre>
  </div>
</template>
