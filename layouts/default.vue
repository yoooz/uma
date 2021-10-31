<template>
  <v-app dark>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-spacer />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [],
      miniVariant: false,
      right: false,
      rightDrawer: false,
      title: '天皇賞 秋(G1)',
    }
  },
}
</script>
