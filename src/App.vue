<template>
    <div class="posts">
        <v-article v-for="post in posts" :post="post" :key="post"></v-article>
    </div>
</template>

<script>
    import VArticle from './components/v-article'

    export default {
        name: 'App',
        components: {
            VArticle,
        },
        data() {
            return {
                posts: []
            }
        },
        created() {
            fetch('http://localhost:3000/data')
                .then(res => res.json())
                .then(data => {
                    this.posts = data
                })
        },
    }
</script>

<style>

</style>
