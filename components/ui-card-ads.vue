<template>
    <article>
      <div class="ui-card-illustration">
        <img :src="img.src" :alt="img.alt">
      </div>
      <h1>{{title}}</h1>
      <div class="ui-card-description">
        <slot></slot>
      </div>
      <NuxtLink :to="link">Voir plus</NuxtLink>
    </article>
</template>

<script>
export default {
  name: "ui-card-ads",
  props: {
    title:{
      type: String,
      default: "Titre de l'annonce"
    },
    img:{
      type: Object,
    },
    link:{
      type: String,
    }
  },
}
</script>

<style scoped>
  article{
    display: flex;
    flex-direction: column;
    height: 250px;
    padding: 1em;

    border-radius: 10px;
    box-shadow: rgba(0,0,0, 0.1) 0 0 15px;
  }

  a{
    display: block;
    text-align: right;
    margin-top: auto;

    color: #0c4dd3
  }

  h1{
    margin: .7em 0;
  }

  .ui-card-illustration{
    width: 100%;
    height: 7em;
  }

  .ui-card-illustration img{
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

</style>
