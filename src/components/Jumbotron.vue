<template>
    <div id="jumbotron" class="w-100">
        <div class="d-flex ">
          <DiceD6 color="green" dotColor="white"/>
          <DiceD6 color="red" dimension="50"/>
          <DiceD6 color="yellow" dimension="200"/>
        </div>
    </div>
</template>

<script>
import DiceD6 from './DiceD6.vue'
 export default {
    name: 'Jumbotron',  
    components: {
DiceD6
    },
    data() {
      
    }
  }
</script>

<style lang="scss" scoped>
#jumbotron {
    height: 50vh;
    width: 100vw;
    background-image: url('/jumbotron.jpg');
    background-repeat: no-repeat;
    background-size: cover;
}

</style>