<template>
    <div>
        <div>Jokes</div>
        <div><Search @search-text="searchText"/></div>
        <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke"/>
    </div>
    
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke.vue'
import Search from '../../components/Search.vue'
export default {
    components: {
        Joke,
        Search
    },
    data() {
        return {
            jokes: []
        }
    },
    async created () {
        let config = {
            headers: {Accept: "application/json"}
        }
        try {
            let res = await axios.get('https://icanhazdadjoke.com/search', config)
            console.log(res)
            this.jokes = res.data.results
        }
        catch (err) {
            console.log(err)
        }
    },
    methods: {
        async searchText (text) {
            let config = {
                headers: {Accept: "application/json"}
            }
            try {
                let res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config)
                console.log(res)
                this.jokes = res.data.results
            }
            catch (err) {
                console.log(err)
            }
        }
    },
    head () {
        return {
            title: "Dad Jokes",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Funny dad jokes you can get ever"
                }
            ]
        }
    }
}
</script>

<style scoped>

</style>