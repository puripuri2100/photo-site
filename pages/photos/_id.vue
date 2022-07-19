<template>
  <v-app>
    <v-row justify="center" align="center">
      <v-col justify="center" align="center">
        <v-card class="pa-10">
          <keep-alive>
            <v-img
              :src="photo_data.photo_src"
              :lazy-src="photo_data.photo_lazy_src"
              :alt = "photo_data.alt"
              max-height="600"
              max-width="600"
              contain
              class="pa-20"
            ></v-img>
          </keep-alive>
          <v-row>
            <v-col justify="start" align="start">
              <v-btn v-if="before_photo" :to="{name: 'photos-id', params:{id: before_photo}, query:{group: group_id}}" x-large>&lt;</v-btn>
            </v-col>
            <v-col justify="start" align="center">
              {{ photo_data.year }}-{{ photo_data.month }}-{{ photo_data.day }} <span v-if="photo_data.hour">{{ photo_data.hour }}:{{ photo_data.minutes }}</span>
              <br>
              <span v-if="photo_data.location">{{ photo_data.location }}</span>
            </v-col>
            <v-col justify="start" align="end">
              <v-btn v-if="after_photo" :to="{name: 'photos-id', params:{id: after_photo}, query:{group: group_id}}" x-large>&gt;</v-btn>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-app>
</template>


<script>
import groupData from '../../static/group_data.json'
import photoData from '../../static/photo_data.json'


var get_photo_data = function (photo_id) {
  return photoData.find(v => v.photo_id === photo_id)
}

var get_before_photo = function (photo_id, group_id) {
  if (group_id == null) {
    for (let i = 0; i < photoData.length; i++) {
      if (photoData[i].photo_id === photo_id) {
        if (i == 0) {} else {
          return photoData[i - 1].photo_id;
        }
      }
    }
    return null;
  } else {
    const group_data = groupData.find(v => v.group_id === group_id);
    const photo_id_list = group_data.photo_id_list;
    for (let i = 0; i < photo_id_list.length; i++) {
      if (photo_id_list[i] === photo_id) {
        if (i == 0) {
        } else {
          return photo_id_list[i - 1];
        }
      }
    }
    return null;
  }
}

var get_after_photo = function (photo_id, group_id) {
  if (group_id == null) {
    const len = photoData.length;
    for (let i = 0; i < len; i++) {
      if ((photoData[i]).photo_id === photo_id) {
        if (i == (len - 1)) {} else {
          return photoData[i + 1].photo_id;
        }
      }
    }
    return null;
  } else {
    const group_data = groupData.find(v => v.group_id === group_id);
    const photo_id_list = group_data.photo_id_list;
    const len = photo_id_list.length;
    for (let i = 0; i < len; i++) {
      if (photo_id_list[i] === photo_id) {
        if (i == (len - 1)) {
        } else {
          return photo_id_list[i + 1];
        }
      } else {
      }
    }
    return null;
  }
}


export default {
  data() {
    return {
      group_id: this.$route.query.group,
      photo_data: get_photo_data(this.$route.params.id),
      before_photo: get_before_photo(this.$route.params.id, this.$route.query.group),
      after_photo: get_after_photo(this.$route.params.id, this.$route.query.group),
    }
  }
}
</script>
