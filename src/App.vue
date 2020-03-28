<template>
  <v-app>
    <v-app-bar color="teal"
      dense
      app
      dark>
      <v-toolbar-title>StreamUI PKP</v-toolbar-title>
    </v-app-bar>
    <v-content>
      <hello-world></hello-world>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
