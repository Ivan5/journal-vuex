<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Hola mndo</h1>
    <button @click="gotoDaybook" class="btn btn-primary">Daybook</button>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {
    
  },
  methods: {
      gotoDaybook(){
        this.$router.push({name: 'no-entry'})
      }
    }
}
</script>
