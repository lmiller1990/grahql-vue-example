<template>
  <div id="app">
    <h3>Example 1</h3>
    <div>
      Data: {{ example1 }}
    </div>
    <button @click="getLanguage">Get Language</button>
    <hr>
    
    <h3>Example 2</h3>
    <div>
      Data:
      <div v-for="champion in champions">
        {{ champion }}
      </div>
    </div>
    <button @click="getChampions">Get Champions</button>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',

  data () {
    return {
      example1: '',
      champions: []
    }
  },

  methods: {
    async getChampions () {
      const res = await axios.post('http://localhost:4000/graphql', {
        query: `{ 
          getChampions { 
            name 
          } 
        }`
      })
      this.champions = res.data.data
    },

    async getLanguage () {
      try {
        const res = await axios.post('http://localhost:4000/graphql', {
        query: '{ language }'
      })
        this.example1 = res.data.data.language
      } catch (e) {
        console.log('err', e)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
