<template>
  <div>
    <h1>Articles</h1>
    <ul>
      <li v-for="(article, index) in articles" :key="index">
        <nuxt-link :to="`/blog/${article.attributes.slug}`">{{ article.attributes.title }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  asyncData () {
    const articles = []
    const r = require.context('~/articles', false, /\.md/)
    r.keys().forEach((key) => {
      articles.push(r(key))
    })
    return {
      articles
    }
  }
}
</script>