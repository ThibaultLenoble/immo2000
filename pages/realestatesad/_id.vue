<template>
  <main>
    <common-layout-header />
    <section>
      <h1>{{this.realestatesAd.title}}</h1>
      <span>{{this.realestatesAd.price}}&nbsp;€ pour {{this.realestatesAd.indoor_surface + this.realestatesAd.outdoor_surface}}&nbsp;m<sup>2</sup></span>
      <p>{{this.realestatesAd.description}}</p>
      <span>{{this.realestatesAdAdress}}, {{this.realestatesAdLocalisation.code}} {{this.realestatesAdLocalisation.name}}</span>
      <ui-slider>
        <li v-for="image in this.realestatesAdImages">
          <img :src="'http://localhost:1337' + image.attributes.url" :alt="image.attributes.alternativeText">
        </li>
      </ui-slider>
    </section>
    <section>
      <h2>Information sur le bien</h2>
      <ul>
        <li>à Vendre : {{this.realestatesAd.isForSale}}</li>
        <li>Meublé : {{this.realestatesAd.isFurnished}}</li>
        <li>Surface intérieur : {{this.realestatesAd.indoor_surface}}&nbsp;m<sup>2</sup></li>
        <li>Surface extérieur : {{this.realestatesAd.outdoor_surface}}&nbsp;m<sup>2</sup></li>
        <li>Nb de pièces : {{this.realestatesAd.room_count}}</li>
        <li>Nb de chambres : {{this.realestatesAd.bedroom_count}}</li>
      </ul>
    </section>
    <common-layout-footer />
  </main>
</template>

<script>
var {graphql, buildSchema} = require('graphql');
export default {
  data(){
    return {
      realestatesAd: Object,
      realestatesAdImages: Array,
      realestatesAdAdress: Object,
      realestatesAdLocalisation: Object,
    }
  },
  methods: {
    getRealestatesAd() {
      fetch('http://localhost:1337/graphql', {
        method: 'POST',
        body: JSON.stringify({
          query: `query{
  realestate(id: `+ this.$route.params.id +`){data{attributes{title, description,price, indoor_surface, outdoor_surface, room_count, bedroom_count, isFurnished, isForSale, publishedAt, images{data{attributes{url, alternativeText}}}, Localisation{adress, adress_complement, localisation{data{attributes{name, region, code, country}}}}}}}
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
          this.realestatesAd = realestateAd.data.realestate.data.attributes
          this.realestatesAdImages = realestateAd.data.realestate.data.attributes.images.data
          this.realestatesAdAdress = realestateAd.data.realestate.data.attributes.Localisation.adress
          this.realestatesAdLocalisation = realestateAd.data.realestate.data.attributes.Localisation.localisation.data.attributes
        })
      });
    }
  },
  mounted() {
    this.getRealestatesAd()
  }
}
</script>
