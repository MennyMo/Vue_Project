<template>
<div>  
  <div>
      <!-- <Main /> -->
  </div>
  <div class="latest-news">
    <h3>Latest News</h3>
  </div>

    <!-- <select class="custom-select" name="categories" id="inputGroupSelect01" v-on:change='onChange($event)'>
      <option selected>Select other category</option>
      <option class="select-header" value="general">General</option>
      <option class="select-header" value="health">Health</option>
      <option class="select-header" value="science">Science</option>
      <option class="select-header" value="sports">Sports</option>
      <option class="select-header" value="entertainment">Entertainment</option>
      <option class="select-header" value="tech">Technology</option>
      <option class="select-header" value="business">Business</option>
    </select> -->

    <select v-model="currentSource" name="category" id="category" class="drop_down custom-select" @change="onChangeMethod($event)">
          <option :value="''">Select category</option>
          <option v-for="{ name, id, url } in getAllSources" :key="id" :value="url">{{ name }}</option>
    </select>
  
   <div class="card-container">
     <div class="card" v-for="allNews in getAllNews" :key="allNews.id">
       <a class="all-links" :href="allNews.url" target="_blank">
            <img v-if="allNews.urlToImage" :src="allNews.urlToImage" class="img" alt="img"/>
            <img v-else :src="imgUrl" class="img" alt="img" />
            <p class="title info">{{allNews.title}}</p>
            <p class="read-more" :href="allNews.url" target="_blank">Read more...</p>
            <p class="info date">Data Published: {{allNews.publishedAt}}</p>
        </a>
        </div>
    </div>

</div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
// import Main from '@/components/Main.vue'
export default {
  name: "Home",
  components: {
    // Main
  },
  data() {
    return {
      imgUrl: 'https://www.9news.com.au/assets/img/9news-image-background.96245abf.jpg',
      currentSource: '',
      currentSourceId: ''
    }
  },
  watch: {
    currentSource(source) {
    const { query: { q }, params } = this.$route;
    const name = this.$route.name
    this.$route.push({ name , params, query: { source, q }});
    }
  },
  computed: {
    ...mapGetters(['getAllNews']),
    ...mapGetters(['getAllSources'])
  },
  mounted() {
    this.fetchAllNews()

    const { params : { category } } = this.$route
    this.fetchAllSources({category}) 
  },
  methods: {
    ...mapActions(['fetchAllNews', 'fetchAllSources']),

    onChangeMethod(event){
        window.open(event.target.value, '_blank');
    }
  }
}
</script>

<style >
 .latest-news {
   padding: 30px;
 }
 h3 {
   margin-top: 20px;
   font-size: 40px;
   font-weight: 500;
 }
 .card-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 40px;
  margin-left: 80px;
  margin-right: 80px;
}
.card {
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 20px 25px -5px, rgba(0, 0, 0, 0.04) 0px 10px 10px -5px;
  display: flex;
  flex-direction: column;
  width: 360px;
  margin-bottom: 60px;
}
.img {
  width: 100%;
  height: 15rem;
  object-fit: cover;
  cursor: pointer;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}
.info {
  text-align: left;
  margin-left: 20px;
  margin-right: 20px;
  cursor: pointer;
  margin-top: 40px;
  margin-bottom: 20px;
}
.card:hover {
  background-color: ghostwhite;
}
.title {
  font-weight: 500;
  font-size: 18px;
  line-height: 27px;
}
.title:hover {
  color: rgb(100, 10, 173);
  text-decoration: blueviolet;
}
.date {
  font-size: 10px;
  font-style: italic;
  color: rgb(90, 9, 138);
}
.read-more {
  text-align: left;
  font-size: 13px;
  margin-left: 20px;
  color: blueviolet;
  font-style: italic;
  text-decoration-line: underline;
}
.all-links {
  text-decoration: none;
}
.custom-select {
  padding: 17px;
  margin-left: 80px;
  margin-right: 80px;
  width: 80%;
  border: none;
  border-radius: 10px;
  outline: none;
  font-family: 'PT Serif Caption';
  font-size: 16px;
  margin-bottom: 17px;
}

.select-header {
  color: rgb(156, 160, 158);
  padding: 20px;
}
</style>
