<template>
  <div>
    <h2>Singleton Comp</h2>
    
  </div>
</template>

<script setup lang="ts">
  class Logger {
    private static instance: Logger;

    //privateなconstructor → 外部からLoggerクラスをインスタンスかできない
    private constructor() {}

    static getInstance() {
      if(!this.instance) {
        this.instance = new Logger();
      }

      return this.instance;
    }

    output(content: string) {
      // const now = new Date();
      // console.log(`${now.toLocaleString('ja-JP')}: ${content}}`)
      console.log('output')
    }
  }

  //singletonが本当にinstanceが一つしかないかどうかを確認するためのテストクラス
  class Test {};

  const run = () => {
    const test1 = new Test();
    const test2 = new Test();
    console.log('Testクラス: ',test1 === test2)

    const logger1 = Logger.getInstance();
    const logger2 = Logger.getInstance();
    console.log('Loggerクラス: ',logger1 === logger2)

    // logger1.output('Logger1のログ')
    // logger2.output('Logger2のログ')

  }

  run();

</script>
