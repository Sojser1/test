<template>
    <div class="posts">
        <v-article v-for="post in posts" :post="post" :key="post"></v-article>
    </div>
    <div class="spinner" v-if="isLoading">
        <v-spinner></v-spinner>
    </div>
    <div class="button" v-if="!isLoading && !isEmpty">
        <button @click="addPostsInList()">Загрузить еще</button>
    </div>

</template>

<script>
    import VArticle from './components/v-article'
    import VSpinner from "./components/v-spinner";

    export default {
        name: 'App',
        components: {
            VSpinner,
            VArticle,
        },
        data() {
            return {
                posts: [],
                isLoading: false,
                data: [],
                isEmpty: false
            }
        },
        created() {
            this.getPosts()
        },
        methods: {
            getPosts() {
                this.isLoading = true
                setTimeout(() => {
                    fetch('http://localhost:3000/data')
                        .then(res => res.json())
                        .then(data => {
                            this.data = data
                            this.addPostsInList()
                        })
                }, 1000)

            },
            addPostsInList() {
                this.isLoading = true
                setTimeout(() => {
                    let i = 0
                    while (i < 10) {
                        if (!this.data[this.posts.length + i]) {
                            this.isLoading = false
                            this.isEmpty = true
                            return
                        }
                        this.posts.push(this.data[this.posts.length + i])
                        i++
                        this.isLoading = false
                    }
                }, 1)
            }
        },
    }
</script>

<style>
    .spinner, .button {
        display: flex;
        margin: 0 auto;
        width: 100vh;
        justify-content: center;
    }

</style>
