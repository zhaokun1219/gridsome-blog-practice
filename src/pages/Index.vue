<template>
  <layout>
    <!-- Page Header -->
    <header 
      class="masthead" 
      :style="{
        backgroundImage: `url(http://localhost:1337${general.cover.url})`
      }"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ general.title }}</h1>
              <span class="subheading">{{ general.subtitle }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key='edge.node.id'>
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">
                {{ edge.node.title }}
              </h2>
            </g-link>
            <p v-if="edge.node.created_by" class="post-meta">Posted by
              <a href="#">{{ edge.node.created_by.firstname + edge.node.created_by.lastname }}</a>
              on {{ edge.node.created_at }}
            </p>
            <p>
              <g-link 
                style="margin-right: 12px" 
                v-for="tag in edge.node.tags" 
                :key='tag.id'
                :to="'/tag/' + tag.id" 
              >
                {{ tag.title }}
              </g-link>
            </p>
            <hr>
          </div>
          <!-- Pager -->
          <Pager class='page-box' :info="$page.posts.pageInfo"/>
          <!-- <div class="clearfix">
            <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
          </div> -->
        </div>
      </div>
    </div>
  </layout>
</template>

<page-query>
  query ($page: Int) {
    posts: allStrapiPost (perPage: 2, page: $page) @paginate {
      pageInfo {
        totalPages
        currentPage
      }
      edges {
        node {
          id
          title
          created_by {
            id
            firstname
            lastname
          }
          created_at
          tags {
            id
            title
          }
        }
      }
    }

    general: allStrapiGeneral {
      edges {
        node {
          id
          title
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
import { Pager } from 'gridsome'

export default {
  name: 'HomePage',
  metaInfo: {
    title: 'Hello, world!'
  },
  components: {
    Pager
  },
  computed: {
    general () {
      return this.$page.general.edges[0].node
    }
  }
}
</script>

<style scoped>
  .page-box a{
    margin-right: 8px;
  }
  .page-box .active{
    color: #0085A1;
  }
</style>
