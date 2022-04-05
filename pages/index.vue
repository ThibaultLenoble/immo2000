<template>
  <main>
    <common-layout-header />
    <ui-section-title :title="'Liste des annonces'" />
    <ui-layout-grid>
      <li v-for="realestatesAd in realestatesAds">
        <ui-card-ads :title="realestatesAd.attributes.title" :img="{src:'http://localhost:1337' + realestatesAd.attributes.images.data[0].attributes.url, alt:realestatesAd.attributes.images.data[0].attributes.alternativeText}" :link="'/realestatesad/' + realestatesAd.id">
          <span>{{realestatesAd.attributes.price}}&nbsp;€</span>
        </ui-card-ads>
      </li>
    </ui-layout-grid>
    <common-layout-footer />
  </main>
</template>

<script>
var {graphql, buildSchema} = require('graphql');

export default {
  name: 'IndexPage',
  components: {},

  data(){
    return {
      realestatesAds: Object,
    }
  },
  methods: {
    getRealestatesAd() {
      fetch('http://localhost:1337/graphql', {
        method: 'POST',
        body: JSON.stringify({
          query: `query{
  realestates{data{id,attributes{title,images{data{attributes{url, alternativeText}}}, publishedAt, price}}}
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
          this.realestatesAds = realestateAd.data.realestates.data
        })
      });
    }
  },
  mounted() {
    this.getRealestatesAd()
  }
}
</script>
