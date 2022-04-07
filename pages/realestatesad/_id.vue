<template>
  <main>
    <common-layout-header />
    <h1>{{this.realestatesAd.title}}</h1>
    <section>
      <div class="basic-informations">
        <span><em>{{realestatesAdAdress}}, {{realestatesAdLocalisation.code}} {{realestatesAdLocalisation.name}}</em></span><br>
        <span>{{realestatesAd.price}}&nbsp;€ pour {{realestatesAd.indoor_surface + realestatesAd.outdoor_surface}}&nbsp;m<sup>2</sup></span>
        <p>{{realestatesAd.description}}</p>
      </div>
      <div class="ads-illustrations">
        <ui-slider>
          <li v-for="image in realestatesAdImages">
            <img :src="'http://localhost:1337' + image.attributes.url" :alt="image.attributes.alternativeText">
          </li>
        </ui-slider>
      </div>
    </section>
    <section>
      <h2>Information sur le bien</h2>
      <ul>
        <li>à Vendre : {{realestatesAd.isForSale}}</li>
        <li>Meublé : {{realestatesAd.isFurnished}}</li>
        <li>Surface intérieur : {{realestatesAd.indoor_surface}}&nbsp;m<sup>2</sup></li>
        <li>Surface extérieur : {{realestatesAd.outdoor_surface}}&nbsp;m<sup>2</sup></li>
        <li>Nb de pièces : {{realestatesAd.room_count}}</li>
        <li>Nb de chambres : {{realestatesAd.bedroom_count}}</li>
      </ul>
    </section>
    <section>
      <ui-contact-ads :ad-id="$route.params.id" />
    </section>
    <common-layout-footer />
  </main>
</template>

<script>
var {graphql, buildSchema} = require('graphql');
export default {
  components: {},

  data(){
    return {
      realestatesAd: {},
      realestatesAdImages: [],
      realestatesAdAdress: {},
      realestatesAdLocalisation: {},
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

<style scoped>
  section{
    padding: 2em;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin: 2em 5em;

    box-shadow: rgba(0,0,0, 0.1) 0 0 15px;
    border-radius: 10px;
  }

  h1{
    font-size:  2em;
    width: 100%;
    padding: 2.5em;
    padding-top: 1em;
    padding-bottom: 0;
  }

  h2{
    width: 100%;
  }

  p{
    margin: 2em 0;
  }

  .basic-informations{
    width: 50%;
  }

  .ads-illustrations{
    width: 50%;

    border: 1px solid lightgray;
  }

  ul{
    margin: 1em 0;
  }
</style>
