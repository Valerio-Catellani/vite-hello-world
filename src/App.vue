<template>
  <div id="card-container" class="d-flex flex-column container align-items-center">
        <TitleComponent/>
        <Jumbotron/>
        <p>click on dice to roll</p>
  </div>
</template>

<script>
import Jumbotron from './components/Jumbotron.vue';
import TitleComponent from './components/TitleComponent.vue';
  export default {
    name: 'App',
    components: {
      Jumbotron,
      TitleComponent,
    },
    data() {
      
    }
  }
</script>

<style lang="scss" scoped>
#card-container {
  height: 100vh;
}

</style>