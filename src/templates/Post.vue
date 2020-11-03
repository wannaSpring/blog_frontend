<template>
    <Layout>
        <!-- Page Header -->
        <header
                class="masthead"
                :style="{
                    backgroundImage: `url(${GRIDSOME_API_URL + $page.post.img.url})`
                }"
        >
            <div class="overlay"></div>
            <div class="container">
                <div class="row">
                    <div class="col-lg-8 col-md-10 mx-auto">
                        <div class="post-heading">
                            <h1>{{$page.post.title}}</h1>
                            <h2 class="subheading">{{$page.post.title}}</h2>
                            <span class="meta">Posted by
              <a href="#">{{$page.post.created_by.firstname + $page.post.created_by.lastname}}</a>
              on {{moment($page.post.created_at)}}</span>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Post Content -->
        <article>
            <div class="container">
                <div class="row">
                    <div
                            class="col-lg-8 col-md-10 mx-auto"
                            v-html="mdToHtml( $page.post.content)"></div>
                </div>
            </div>
        </article>

        <hr>
    </Layout>
</template>
<page-query>
    query($id: ID!) {
    post : strapiBlog(id: $id) {
    id
    title
    content
    created_by{
    id
    firstname
    lastname
    }
    tags {
    title
    }
    created_at
    img {
    url
    }
    }
    }
</page-query>
<script>
  import moment from 'moment'
  import MarkdownIt from 'markdown-it'

  const md = new MarkdownIt();
  export default {
    name: "Post",
    methods: {
      moment: function (date) {
        return moment(date).format('YYYY-MM-DD')
      },
      mdToHtml(markdown) {
        return md.render(markdown)
      }
    }
  }
</script>

<style scoped>

</style>
