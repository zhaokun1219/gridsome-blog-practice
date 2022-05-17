<template>
  <Layout>
    <!-- Page Header -->
    <header 
      class="masthead" 
      :style="{
        backgroundImage: `url(${GRIDSOME_ASSET_URL}${aboutme.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="page-heading">
              <h1>{{aboutme.title}}</h1>
              <span v-if="aboutme.subtitle" class="subheading">{{aboutme.subtitle}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto" v-html="mdToHtml(aboutme.content)">
          
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query {
    aboutme: allStrapiAboutme {
      edges {
        node {
          title
          content
          subtitle
          cover {
            url
          }
        }
      }
    }
  }
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()
export default {
  name: 'About',
  computed: {
    aboutme () {
      return this.$page.aboutme.edges[0].node
    }
  },
  methods: {
    mdToHtml (markdown) {
      return md.render(markdown)
    }
  }
}
</script>
