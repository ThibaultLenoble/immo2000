<template>

  <div>
    <div v-for="ad in realestatesAd">
      {{ad.attributes.title}}
    </div>
  </div>
</template>

<script>
var {graphql, buildSchema} = require('graphql');
export default {
  data(){
    return {
      realestatesAd: Object,
    }
  },
  methods: {
    getRealestatesAd() {
      fetch('http://localhost:1337/graphql', {
        method: 'POST',
        body: JSON.stringify({
          query: `query{
  realestates{data{id, attributes{title, publishedAt}}}
}`,
          variables: {
            type: 'post'
          }
        }),
        headers: {
          'content-type': 'application/json'
        }
      }).then(async (data) => {
        // Console log our return data
        await data.json().then(realestateAd =>{
          this.realestatesAd = realestateAd.data.realestates.data
        })
      });
    }
  },
  mounted() {
    this.getRealestatesAd()
  }
}
</script>
