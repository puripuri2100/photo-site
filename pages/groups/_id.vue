<template>
  <v-app>
    <h1>{{ title }}</h1>
    <p>{{ description }}</p>
    <v-container>
      <v-row justify="center" align="center">
        <v-col v-for="(item, i) in photoDataList" :key="i"  md="6" sm="12">
          <v-card
          elevation="50"
          height="430"
          class="pa-15"
          link
          :to="{name: 'photos-id', params:{id: item.photo_id}, query:{group: groupId}}"
          >
            <v-container>
              <v-row justify="center" align="center" class="pa-5">
                <keep-alive>
                  <v-img
                    :src="item.photo_src"
                    :lazy-src="item.photo_lazy_src"
                    :alt = "item.alt"
                    max-height="200"
                    contain
                  ></v-img>
                </keep-alive>
              </v-row>
              <v-row justify="center" align="center" class="pa-5">
                <v-container>
                  <v-row justify="center" align="center">
                  {{ item.year }}-{{ item.month }}-{{ item.day }}
                  </v-row>
                  <v-row justify="center" align="center">
                  {{ item.location }}
                  </v-row>
                </v-container>
              </v-row>
            </v-container>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>


<script>
import groupData from '../../static/group_data.json'
import photoData from '../../static/photo_data.json'

var get_group_data = function (group_id) {
  return groupData.find(v => v.group_id == group_id)
}
var get_photo_data = function (photo_id) {
  return photoData.find(v => v.photo_id == photo_id)
}

export default {
  data() {
    return {
      showFullscreen: false,
      title: get_group_data(this.$route.params.id).title,
      groupId: this.$route.params.id,
      description: get_group_data(this.$route.params.id).description,
      photoDataList: get_group_data(this.$route.params.id).photo_id_list.map(v => get_photo_data(v)),
      photoListSize: get_group_data(this.$route.params.id).photo_id_list.length
    }
  },
  methods: {
    close() {
      // フルスクリーンを停止
      this.showFullscreen = false;
    }
  }
}
</script>
