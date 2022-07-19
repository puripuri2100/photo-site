<template>
<v-app>
  <v-container>
  <v-row justify="center" align="center">
    <v-col v-for="(item, i) in group_list" :key="i" md="6" sm="12">
      <v-card
      elevation="50"
      height="430"
      class="pa-15"
      link
      :to="{name: 'groups-id', params:{id: item.group_id}}"
      >
        <v-row justify="center" align="center" class="pa-5">
          <keep-alive>
            <v-img
              :src="search_photo_by_id(item.photo_id_list[0])"
              :lazy-src="search_lazy_photo_by_id(item.photo_id_list[0])"
              :alt = "item.title"
              max-height="200"
              contain
            ></v-img>
          </keep-alive>
        </v-row>
        <v-row justify="center" align="center" class="pa-5">
          <v-container>
            <v-row justify="center" align="center">
              {{ item.title }}
            </v-row>
            <v-row justify="center" align="center">
            {{ item.year }}-{{ item.month }}-{{ item.day }}
            </v-row>
            <v-row justify="center" align="center">
            {{ item.location }}
            </v-row>
          </v-container>
        </v-row>
      </v-card>
  </v-col>
  </v-row>
  </v-container>
</v-app>
</template>

<script>
import groupData from '@/assets/group_data.json'
import photoData from '@/assets/photo_data.json'

export default {
  group_id: 'IndexPage',
  data() {
    return {
      group_list: groupData,
      photo_list: photoData

    }
  },
  methods: {
    search_photo_by_id(head_id) {
      return (this.photo_list.find(v => v.photo_id === head_id)).photo_src
    },
    search_lazy_photo_by_id(head_id) {
      return (this.photo_list.find(v => v.photo_id === head_id)).photo_lazy_src
    }
  }
}
</script>
