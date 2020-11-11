<template>
    <layout>

        <!-- Page Header -->
        <header 
            class="masthead"
            :style="{
              backgroundImage: `url(${GRIDSOME_API_URL + general.banner.url})`
            }"
        >
            <div class="overlay"></div>
            <div class="container">
                <div class="row">
                    <div class="col-lg-8 col-md-10 mx-auto">
                        <div class="site-heading">
                            <h1>{{general.title}}</h1>
                            <span class="subheading">{{general.subTitle}}</span>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <div class="container">
            <div class="row">
                <div class="col-lg-12 col-md-10 mx-auto">
                    <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
                        <g-link :to="'/post/' + edge.node.id ">
                            <h3 class="post-title">
                                {{edge.node.title}}
                            </h3>
                            <p class="post-meta">Posted by
                                <a href="#">{{'望春'}}</a>
                                on {{format(edge.node.created_at)}}
                            </p>
                        </g-link>
                      
                        <p class= 'tag'>
                          文章标签：
                          <span  v-for="tag in edge.node.tags" :key="tag.id">
                            <g-link :to="/tag/ + tag.id" >{{tag.title}}</g-link>
                            &nbsp; &nbsp;
                          </span>
                        </p>
                        <hr>
                    </div>
                    <!-- Pager -->
                    <Pager :info="$page.posts.pageInfo" class="pager"/>
                </div>
            </div>
        </div>
        <hr>
    </layout>
</template>
<style >
    .pager a{
        display: inline-flex;
        justify-content: center;
        align-items: center;
        margin-right: 10px;
        width: 50px;
        height: 50px;
        font-size: 16px;
    }
    .pager a:hover{
        color: #00A672;
        border-bottom: 1px solid #00A672;
    }
    .active--exact{
        color: #00A672;
        border-bottom: 1px solid #00A672;
    }
    .tag {
        color: #8fafd7;
        font-size: 12px;
    }
</style>
<page-query>
query ($page: Int) {
allStrapiGeneral {
edges {
node {
title
subTitle
banner {
url
}
}
}
}
posts: allStrapiBlog (perPage:6, page: $page)@paginate {
pageInfo {
totalPages
currentPage
}
edges {
node {
id
title
content
created_at
tags {
title
id
}
}
}
}
}
</page-query>

<script>
  import { Pager } from 'gridsome'
  import dayjs from 'dayjs'
  export default {
    name: 'Home',
    metaInfo: {
      title: 'Hello, world!'
    },
    components: {
      Pager
    },
    methods: {
        format(date) {
            return dayjs(date).format('YYYY-MM-DD')
        }
    },
    computed: {
        general() {
            console.log(this.$page.allStrapiGeneral.edges[0].node.banner.url, 'this.$page.general')
            return this.$page.allStrapiGeneral.edges[0].node
        }
    }
  }
</script>
