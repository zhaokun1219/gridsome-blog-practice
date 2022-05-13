<template>
  <layout>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{ $page.tag.title }}</h1>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="post in $page.tag.posts" :key='post.id'>
            <g-link :to="'/post/' + post.id">
              <h2 class="post-title">
                {{ post.title }}
              </h2>
            </g-link>
            <!-- <p v-if="post.created_by" class="post-meta">Posted by
              <a href="#">{{ post.created_by.firstname + post.created_by.lastname }}</a>
              on {{ post.created_at }}
            </p>
            <p>
              <g-link 
                style="margin-right: 12px" 
                v-for="tag in post.tags" 
                :key='tag.id'
                :to="'/tag/' + tag.id" 
              >
                {{ tag.title }}
              </g-link>
            </p> -->
            <hr>
          </div>
          <!-- Pager -->
          <!-- <Pager class='page-box' :info="$page.posts.pageInfo"/> -->
        </div>
      </div>
    </div>
  </layout>
</template>

<page-query>
  query ($id: ID!) {
    tag: strapiTag (id: $id) {
      id
      title
      posts {
        id
        title
      }
    }
  }
</page-query>

<script>
  export default {
    name: 'TagPage',
    data: function() {
      return {}
    },
  }
</script>

<style scoped>

</style>