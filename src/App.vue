<template>
    <div class="posts">
        <v-test v-for="post in posts" :post="post" :key="post"></v-test>
    </div>
</template>

<script>
    import VTest from './components/test'

    export default {
        name: 'App',
        components: {
            VTest,
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
