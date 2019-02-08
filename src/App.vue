<template>
  <div id="app">
    <NavBar v-if="showNav" :molgenis-menu="molgenisMenu"/>
    <div class="container">
      <HelloWorld/>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import api from '@molgenis/molgenis-api-client'
import NavBar from '@molgenis/molgenis-ui-context/src/components/NavBar'

export default Vue.extend({
  name: 'app',
  components: {
    HelloWorld, NavBar
  },
  data () {
    return {
      molgenisMenu: {},
      showNav: false
    }
  },
  mounted () {
    api.get('/plugin/app-ui-context').then((context) => {
      this.molgenisMenu = context
      this.showNav = true
    })
  }
})
</script>
