<template>
  <div id="app">
    <NavBar v-if="isContextLoaded" :molgenis-menu="molgenisMenu"/>
    <div class="container">
      <HelloWorld/>
    </div>
    <FooterComponent v-if="isContextLoaded" :molgenisFooter="footerData"/>
  </div>
</template>

<script>
import Vue from 'vue'
import api from '@molgenis/molgenis-api-client'
import NavBar from '@molgenis/molgenis-ui-context/src/components/NavBar'
import FooterComponent from '@molgenis/molgenis-ui-context/src/components/FooterComponent'
import HelloWorld from './components/HelloWorld.vue'

export default Vue.extend({
  name: 'app',
  components: {
    HelloWorld, NavBar, FooterComponent
  },
  data () {
    return {
      molgenisMenu: {},
      footerData: {},
      isContextLoaded: false
    }
  },
  mounted () {
    api.get('/plugin/app-ui-context').then((context) => {
      this.molgenisMenu = context
      this.footerData = context
      this.isContextLoaded = true
    })
  }
})
</script>
