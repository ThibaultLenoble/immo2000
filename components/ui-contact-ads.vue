<template>
  <form method="POST" @submit="send">
    <form-ui-input-text v-model="emailValue" id="email" label="email" type="email" name="email" placeholder="Votre email"/>
    <!-- your other form fields go here -->
    <input type="hidden" name="ad-id" :value="adId">
    <input type="hidden" name="ad-url" :value="adUrl">
    <form-ui-button type="submit" label="Envoyer"/>
  </form>
</template>

<script>

const axios = require('axios').default;


export default {
  name: "ui-contact-ads",
  props: {
    adId: "",
  },
  data() {
    return {
      emailValue : '',
      adUrl: '',
    }
  },
  methods:{
    send(e){
      e.preventDefault()
      axios({
        url: 'https://formspree.io/f/mzboanwe',
        method: 'post',
        headers: {
          'Accept': 'application/json'
        },
        data: {
          email: this.$data.emailValue,
          ad: this.adId,
          url: this.adUrl
        }
      })
    },
  },
  mounted() {
    this.adUrl = location.protocol + '//' + location.host + '/realestatesad/' + this.adId
  }
}
</script>

<style scoped>

</style>
