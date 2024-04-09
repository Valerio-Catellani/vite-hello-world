<template>
    <div>
        <h1 class="text-center py-5">{{ title }}</h1>
    </div>
</template>

<script>
 export default {
    name: 'TitleComponent',  

    data() {
      return {
        title: 'Hello World!'
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>