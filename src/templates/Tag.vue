<template>
    <layout>

        <!-- Page Header -->
        <header 
            class="masthead" 
            :style="{
                backgroundColor: `${color16}`
            }"
        >
            <div class="overlay"></div>
            <div class="container">
                <div class="row">
                    <div class="col-lg-8 col-md-10 mx-auto">
                        <div class="site-heading">
                            <h1>{{ $page.tag.title}}</h1>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <div class="container">
            <div class="row">
                <div class="col-lg-8 col-md-10 mx-auto">
                    <div class="post-preview" v-for="post in $page.tag.blogs" :key="post.id">
                        <g-link :to="'/post/' + post.id ">
                            <h2 class="post-title">
                                {{post.title}}
                            </h2>
                        </g-link>
                        <p class="post-meta">Posted by
                            <a href="#">{{post.created_by}}</a>
                            on {{post.created_at}}
                        </p>
                        <hr>
                    </div>
                    <!-- Pager -->
                </div>
            </div>
        </div>
        <hr>
    </layout>
</template>
<page-query>
    query($id:ID!) {
        tag: strapiTag(id:$id){
            id
            title
            blogs{
                title
                id
                created_by
                created_at
            }
        }
    }
</page-query>
<script>
  export default {
    name: "TagPage",
    computed: {
        color16(){//十六进制颜色随机
			var r = Math.floor(Math.random()*256);
			var g = Math.floor(Math.random()*256);
			var b = Math.floor(Math.random()*256);
            var color = '#'+r.toString(16)+g.toString(16)+b.toString(16);
            console.log(color, 'color')
			return color;
		}
    }
  }
</script>

<style scoped>

</style>
