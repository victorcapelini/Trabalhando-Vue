<template>
    <nav>
      <ul>       
          <li v-for="rota in rotas">
            <router-link :to="rota.path">{{ rota.titulo }}</router-link>
          </li>
      </ul>
    </nav>
</template>
<script>
export default {
  props: {
    rotas: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
li {
  display: inline-block;
  margin-left: 0.5em;
  margin-right: 0.5em;
}
</style>
