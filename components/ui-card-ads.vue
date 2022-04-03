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
