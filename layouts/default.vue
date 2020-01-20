<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import 'chart.js'
import 'hchs-vue-charts'

export default {
  data() {
    return {
      title: "Photo_detail"
    };
  }
};
</script>
