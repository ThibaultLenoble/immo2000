<template>
  <header>
    <nuxt-link to="/"><h1>Immo 2000</h1></nuxt-link>
    <nav>
      <ul>
        <li><nuxt-link to="/">Liste des annonces</nuxt-link></li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: "layout-header"
}
</script>

<style scoped>
  header{
    display: flex;
    flex-direction: row;
    align-items: center;
    padding: 1.5em 2em;

    box-shadow: rgba(0,0,0, 0.1) 0 5px 5px;
  }

  nav{
    margin-left: 1em;
  }

  nav ul{
    display: flex;
    flex-direction: row;
    list-style-type: none;
  }

  a{
    color: #0c4dd3
  }
</style>
