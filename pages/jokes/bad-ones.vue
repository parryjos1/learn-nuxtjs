<template>
    <div>
        <h3>The really bad ones</h3>
        <div>
            <Joke 
                v-for="joke in jokes" 
                :key="joke.id"
                :id="joke.id"
                :joke="joke.joke"
            />
        </div>

    </div>
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke'

export default {
    components: {
        Joke
    },

    data(){
        return{
            jokes: [],
        }
    },
    async created(){
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }
        try {
            const res = await axios.get("https://icanhazdadjoke.com/search", config);
            this.jokes = res.data.results
        } catch (error) {
            console.log(error)
        }

    }
}
</script>

<style>

</style>