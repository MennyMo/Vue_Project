<template>
  <div>
      <div class="news-item">
          <div class="news-source">
              <h1>{{ story.source && story.source.name }} </h1>
          </div>
          <div class="news-headline">
              <h2>{{ story.title }} </h2>
          </div>
          <div class="news-content">
              <p v-if="story.content !== null"> {{ story.content }} </p>
              <p v-else> Some content due to API returning null</p>
          </div>
          <div class="news-action">
              <a :href="story.url" target="_blank" rel="noreferer noopener" class="news_button">More News</a>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'NewsItem',
    props: {
        story: {
            type: Object,
            required: true
        }
    }

}
</script>

<style>

</style>