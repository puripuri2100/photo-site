<template>
<v-app>
  <v-row justify="center" align="center">
    <v-col v-for="(item, i) in photoList" :key="i" md="6" sm="12">
      <v-card
      elevation="50"
      class="pa-15"
      min-width="300"
      link
      :to="{name: 'photos-id', params:{id: item.photo_id}}"
      >
        <v-row justify="center" align="center">
          <keep-alive>
            <v-img
              :src="item.photo_src"
              :lazy-src="item.photo_src"
              :alt = "item.alt"
              max-height="200"
              contain
            ></v-img>
          </keep-alive>
        </v-row>
      </v-card>
    </v-col>
  </v-row>
</v-app>
</template>

<script>
import photoData from '@/assets/photo_data.json'

export default {
  group_id: 'IndexPage',
  data() {
    return {
      photoList: photoData
    }
  }
}
</script>
