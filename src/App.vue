<template>
  <div id="app">

    <div class="page-load">
      <page-loader />
    </div>

    <div class="page-body">
      <list-machines :machines=machines></list-machines>
    </div>
    
  </div>
</template>

<script>
import ListMachines from './components/ListMachines.vue'
import PageLoader from './components/PageLoader.vue'

export default {
  name: 'app',
  components: { ListMachines, PageLoader },
  data() {
    return {
      machines: []
    }
  },
  created() {
    fetch('../data.json')
    .then((res) => { return res.json() })
    .then((res) => { this.machines=res.machines })
  }
}
</script>

<style scoped>
  #app {

  }
</style>
