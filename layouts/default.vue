<template>
  <v-app light>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
    <nuxt-link to="/" no-prefetch class="ma-5">Top</nuxt-link>
    <nuxt-link :to="{name: 'photos'}" no-prefetch class="ma-5">写真一覧</nuxt-link>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="true"
      app
    >
      <span>&copy; 2022 Naoki Kaneko (a.k.a. "puripuri2100")</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      clipped: false,
      drawer: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'photo-puripuri2100'
    }
  }
}
</script>
