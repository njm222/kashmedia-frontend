<template>
  <v-layout>
    <v-flex class="text-center">
      <v-toolbar height="80" color="#121212">
        <v-toolbar-title>
          Portfolio
        </v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items>
          <v-card-text>
            <v-select
              item-text="name"
              v-model="defaultCategory"
              :label="defaultCategory.name"
              :items="videoCategories"
              class="d-flex align-center"
              solo
              transition="scroll-y-transition"
            ></v-select>
          </v-card-text>
        </v-toolbar-items>
      </v-toolbar>
      <div>
        <v-container>
          <v-row v-for="video in videosByCategory" :key="video.link" cols="12" class="my-8">
            <v-layout>
              <youtube :video-id="video.link" player-width="100%" player-height="100%" class="youtube-container col-5"></youtube>
              <v-layout column class="col-6 offset-1 text-left">
                <v-card-title>{{video.title}}</v-card-title>
                <v-card-text>{{video.description}}</v-card-text>
              </v-layout>
            </v-layout>
          </v-row>
        </v-container>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import videosQuery from '~/apollo/queries/video/videos'
import videoCategoriesQuery from '~/apollo/queries/video/categories'

export default {
  data() {
    return {
      // Initialize an empty videos variable
      model: 'tab-portfolio-videos',
      videos: [],
      videoCategories: [],
      defaultCategory: 'documentary'
    }
  },
  apollo: {
    videos: {
      prefetch: true,
      query: videosQuery
    },
    videoCategories: {
      prefetch: true,
      query: videoCategoriesQuery
    }
  },
  computed: {
    videosByCategory: function () {
      return this.videos.filter((video) => {
        return video.video_categories.some((category) => {
          return category.name === this.defaultCategory
        })
      })
    }
  },
}
</script>

<style>
  .youtube-container {
    width: 100%;
    height: 0;
    margin: auto;
    z-index: 1;
    position: relative;
    padding-bottom: 23.4375%;
    display: block;
    overflow: hidden;
  }
  .youtube-container iframe {
    display: block;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 5;
    position: absolute;
  }
</style>
