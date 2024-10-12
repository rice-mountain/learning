<template>
  <v-responsive class="border rounded">
    <v-app>
      <!-- <v-app-bar title="App bar"></v-app-bar> -->

      <v-navigation-drawer>
        <v-list>
          <v-list-item title="My Application" subtitle="Vuetify"></v-list-item>
          <v-divider></v-divider>
          <v-list-group>
            <!-- v-slot:activator に propsを渡す -->
            <template #activator="{ props }">
              <v-list-item v-bind="props" title="Design Pattern"></v-list-item>
            </template>
            <v-list-item link title="Template Method" to="/designPattern/templateMethod"></v-list-item>
            <v-list-item link title="Singleton" to="/designPattern/singleton"></v-list-item>
            <v-list-item link title="Adapter" to="/designPattern/adapter"></v-list-item>
            <v-list-item link title="Iterator" to="/designPattern/iterator"></v-list-item>
            <v-list-item link title="Factory Method" to="/designPattern/factoryMethod"></v-list-item>
            <v-list-item link title="Facade" to="/designPattern/facade"></v-list-item>
          </v-list-group>
          <v-list-group>
            <template #activator="{ props }">
              <v-list-item v-bind="props" title="JavaScript"></v-list-item>
            </template>
            <v-list-item link title="実行環境" to="/javaScriptBase/runtime"></v-list-item>
            <v-list-item link title="Scope" to="/javaScriptBase/scope"></v-list-item>
            <v-list-item link title="Variable" to="/javaScriptBase/variable"></v-list-item>
            <v-list-item link title="Function and Object" to="/javaScriptBase/function"></v-list-item>
            <v-list-item link title="Loop" to="/javaScriptBase/loop"></v-list-item>
            <v-list-item link title="Async" to="/javaScriptBase/async"></v-list-item>
            <v-list-item link title="module" to="/javaScriptBase/module"></v-list-item>
            <v-list-item link title="Object" to="/javaScriptBase/obj"></v-list-item>
            <v-list-item link title="k" to="/"></v-list-item>
          </v-list-group>
          <v-list-group>
            <v-list-item link title="List Item 3"></v-list-item>
          </v-list-group>
        </v-list>
      </v-navigation-drawer>
      <v-main>
        <v-container>
          <slot />
        </v-container>
      </v-main>
    </v-app>
  </v-responsive>
</template>