<template>
  <v-app dark>
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
      <v-container>
        <RegisterForm/>
        <ReferenceDataTable/>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import RegisterForm from "./components/RegisterForm";
import ReferenceDataTable from "./components/ReferenceDataTable";

export default {
  name: "App",
  components: {
    RegisterForm,
    ReferenceDataTable
  },
  data() {
    return {
      //
    };
  }
};
</script>
