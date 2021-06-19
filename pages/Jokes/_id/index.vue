<template>
    <div>
        Single Joke
        {{ $route.params.id }}
        <nuxt-link to="/jokes">
            Back To Jokes
        </nuxt-link>
        <h2>{{ joke.joke }}</h2>
        <hr />
        <small>Joke ID: {{ $route.params.id }}</small>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data () {
        return {
            joke: {}
        }
    },
    async created () {
        let config = {
            headers: {Accept: "application/json"}
        }
        try {
            let res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config)
            console.log(res)
            this.joke = res.data
        }
        catch (err) {
            console.log(err)
        }
    },
}
</script>

<style scoped>

</style>