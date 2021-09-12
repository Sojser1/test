<template>
 <div class="post">
  <p>{{getTime}}, {{getDate}} / <b>{{post.authorName}}</b> / {{post.authorUrl}}</p>
  <p class="article" v-html=transformString(post.content,post.contentPostTones)>
  </p>
 </div>
 <hr>
</template>

<script>
    export default {
        props: ['post'],
        data() {
            return {}
        },
        created() {
        },
        methods: {
            transformString(string, options) {
                const res = string.split('')

                let i = 0
                for (let option of options) {
                    res.splice(option.position + i, 0, `<span style="background: ${this.getColor(option.tone)}">`)
                    i++
                    res.splice(option.position + option.length + i, 0, `</span>`)
                    i++
                }
                return res.join('')
            },

            getColor(param) {
                if (param === -1) {
                    return 'rgb(255,0,0)'
                } else if (param > -1 && param < 0) {
                    return `rgb(255, ${Math.round(255 * (1 - Math.abs(param)))}, 0)`
                } else if (param === 0) {
                    return 'rgb(255,255,0)'
                } else if (param > 0 && param < 1) {
                    return `rgb(${Math.round(255 * (1 - param))}, 255, 0)`
                } else {
                    return 'rgb(0, 255,0)'
                }
            }
        },
        computed: {
            getDate() {
                const months = ['января', 'февраля', 'марта', 'апреля', 'мая', 'июня', 'июля', 'августа', 'сентября', 'октября', 'ноября', 'декабря']
                const date = new Date(this.post.date)
                const month = months[date.getMonth()]
                const day = date.getDay()
                const year = date.getFullYear()
                return `${day} ${month} ${year}`
            },
            getTime() {
                const date = new Date(this.post.date)
                return date.toLocaleTimeString().slice(0, 5)
            }

        }

    }
</script>