<template>
  <Layout>
    <h1 class="mx-4 mb-4 font-display text-indigo-darker sm:text-center lg:text-left">Tag: {{ $page.wordPressPostTag.title }} </h1>
    <ul class="post-list">
      <li v-for="{ node } in $page.wordPressPostTag.belongsTo.edges" :key="node.id">
        <Post :post="node" />
      </li>
    </ul>
    <Pager :info="$page.wordPressPostTag.belongsTo.pageInfo"/>
  </Layout>
</template>

<page-query>
query Tag ($path: String, $page: Int) {
  wordPressPostTag (path: $path) {
    title
    belongsTo (page: $page, perPage: 9) @paginate {
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          ... on WordPressPost {
            id
            title
            path
            excerpt
        	}
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from 'gridsome'
import Post from '~/components/Post.vue'

export default {
  components: {
    Pager,
    Post
  },
  metaInfo() {
    return {
      title: this.$page.wordPressPostTag.title
    }
  }
}
</script>
