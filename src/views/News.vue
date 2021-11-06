<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="news_grid">
      <div v-if="getLoading">Loading...</div>
      <k-news-item v-else v-for="(headline, index) in getAllNews" :key="index" :story = "headline"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src 
// import HelloWorld from '@/components/HelloWorld.vue'

import kNewsItem from '@/components/NewsItem.vue';
import {mapActions, mapGetters} from 'vuex';


export default {
  name: 'Home',
  components: {
    kNewsItem
  },
  //watch query parameters
  watch: {
    '$route.query': {
      handler: function(val){
        //this.route.params = category(destructuring this to the one below)
        const { params : {category}} = this.route
        const source = val.source
        this.fetchAllNews({category, source})
      },
      deep: true,
      immediate: true
    }
  },
  mounted() {
    const { params : {category}} = this.route
    this.fetchAllNews({category})
  },
  computed: {
    ...mapGetters(['getAllNews','getLoading']),
  },
  methods: {
    ...mapActions(['fetchAllNews'])
  }
}
</script>
