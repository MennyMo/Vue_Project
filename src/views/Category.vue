<template>
  <div>  
  <div>
      <!-- <Main /> -->
  </div>
  <div class="latest-news">
    <h3>Latest News</h3>
  </div>
  
   <div class="card-container">
     <div class="card" v-for="category in getCategoryNews" :key="category.id">
       <a class="all-links" :href="category.url" target="_blank">
            <img v-if="category.urlToImage" :src="category.urlToImage" class="img" alt="img"/>
            <img v-else :src="imgUrl" class="img" alt="img" />
            <p class="title info">{{category.title}}</p>
            <p class="read-more" :href="category.url" target="_blank">Read more...</p>
            <p class="info date">Data Published: {{category.publishedAt}}</p>
        </a>
        </div>
    </div>

</div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'Category',
   data() {
    return {
      imgUrl: 'https://www.9news.com.au/assets/img/9news-image-background.96245abf.jpg'
    }
  },
  watch: {
    '$route.params.category': function (category) {
			this.fetchCategoriesNews(category)
		}
  },
  mounted() {
    const category = this.$route.params.category
    this.fetchCategoriesNews(category)
    // const { params : { category } } = this.$route
    // this.fetchAllNews({category})
  },
  methods: {
    ...mapActions(['fetchCategoriesNews'])
  },
  computed: {
    ...mapGetters(['getCategoryNews'])
  }
}
</script>

<style>

</style>