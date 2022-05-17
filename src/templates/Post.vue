<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{
        'background-image': `url(${GRIDSOME_PROXY_URL}${$page.post.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
              <span v-if="$page.post.created_at" class="meta">{{ $page.post.created_at | date('YYYY-MM-DD')}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="mdToHtml($page.post.content)">
          </div>
        </div>
      </div>
    </article>
  </Layout>
</template>

<page-query>
  query ($id: ID!) {
    post: strapiPost (id: $id) {
      id
      title
      content
      created_at
      cover {
        url
      }
      tags {
        id
        title
      }
    }
  }
</page-query>

<script>
  import MarkdownIt from 'markdown-it'
  const md = new MarkdownIt()

  export default {
    name: 'PostPage',
    data: function() {
      return {}
    },
    methods: {
      mdToHtml (markdown) {
        return md.render(markdown)
      }
    }
  }
</script>

<style>

</style>