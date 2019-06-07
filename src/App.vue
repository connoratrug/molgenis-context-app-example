<template>
  <div id="app" class="mg-page">
    <HeaderComponent v-if="isContextLoaded" :molgenis-menu="molgenisMenu"/>
    <main class="mg-page-content">
      <div class="container">
        <HelloWorld/>
      </div>
    </main>
    <FooterComponent v-if="isContextLoaded" :molgenisFooter="footerData"/>
  </div>
</template>

<script>
import Vue from 'vue'
import api from '@molgenis/molgenis-api-client'
import HeaderComponent from '@molgenis/molgenis-ui-context/src/components/HeaderComponent'
import FooterComponent from '@molgenis/molgenis-ui-context/src/components/FooterComponent'
import HelloWorld from './components/HelloWorld.vue'

export default Vue.extend({
  name: 'app',
  components: {
    HelloWorld, HeaderComponent, FooterComponent
  },
  data () {
    return {
      molgenisMenu: {},
      footerData: {},
      isContextLoaded: false
    }
  },
  mounted () {
    api.get('/app-ui-context').then((context) => {
      this.molgenisMenu = context
      this.footerData = context
      this.isContextLoaded = true
    })
  }
})
</script>
