<template>
  <div>
    <h2>Template Method Comp</h2>
    <DesignPatternTemplateMethodDescription />
  </div>
</template>

<script setup lang="ts">
abstract class TestTemplate {
  test() {
    this.setup();
    this.execute();
    this.tearDown;
  }

  abstract setup(): void;
  abstract execute(): void;
  
  tearDown() {
    console.log("tearDown");
  }
}

class ItemServiceTest extends TestTemplate {
  setup() {
    console.log("setup: ItemServiceTest");
  }
  execute() {
    console.log("execute: ItemServiceTest");
  }
}

class UserServiceTest extends TestTemplate {
  setup() {
    console.log("setup: UserServiceTest");
  }
  execute() {
    console.log("execute: UserServiceTest");
  }
}

const run = () => {
  const itemServiceTest = new ItemServiceTest();
  const userServiceTest = new UserServiceTest();

  itemServiceTest.test();
  userServiceTest.test();
};

run();
</script>
