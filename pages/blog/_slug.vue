<template>
  <article>
    <div v-html="markdown.html" />
  </article>
</template>

<script>
export default {
  head () {
    return {
      title: `${this.markdown.attributes.title}`,
      meta: [
        { hid: 'description', name: 'description', content: this.markdown.attributes.description },
        { property: 'og:title', content: `${this.markdown.attributes.title}` },
        { property: 'og:url', content: `https://your-domain.com${this.$route.fullPath}` },
        { property: 'og:description', content: this.markdown.attributes.description },
        { property: 'og:type', content: 'article' },
        { property: 'article:author', content: 'https://your-domain.com' },
        { property: 'article:publisher', content: 'https://your-domain.com' },
        { property: 'article:published_time', content: this.markdown.attributes.date },
        { property: 'article:tag', content: this.markdown.attributes.tags }
      ]
    }
  },
  asyncData ({route}) {
    const { params: { slug } } = route
    const markdown = require(`~/articles/${slug}.md`)
    return {
      markdown
    }
  },
  jsonld () {
    return {
      '@context': 'http://schema.org',
      '@type': 'Article',
      author: 'Jessie Barnett',
      headline: this.markdown.attributes.title,
      tags: this.markdown.attributes.tags,
      wordcount: this.markdown.html.split(' ').length,
      datePublished: this.markdown.attributes.date,
      description: this.markdown.attributes.description
    }
  }
}
</script>