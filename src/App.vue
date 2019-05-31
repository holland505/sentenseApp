<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline">
        <h1>Sentence</h1>
      </v-toolbar-title>
      <!--
      <v-btn
        flat
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
      -->
    </v-toolbar>

    <v-content>
      <RegisterForm/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import RegisterForm from "./components/RegisterForm";

export default {
  name: "App",
  components: {
    HelloWorld,
    RegisterForm
  },
  data() {
    return {
      //
    };
  }
};
</script>
