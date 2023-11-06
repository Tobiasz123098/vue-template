<template>
    <navbar
      :pages="pages"
      :active-page="activePage"
      :nav-link-click="(index) => activePage = index"
    />
    <!-- <page-viewer
      v-if="pages.length > 0"
      :page="pages[activePage]"
    /> -->

    <create-page
      :page-created="pageCreated"
    />
</template>
<script>
import CreatePage from './components/CreatePage.vue'
import Navbar from './components/Navbar.vue'
import PageViewer from './components/PageViewer.vue'

export default {
  components: { 
    Navbar,
    PageViewer, 
    CreatePage
  },
  created() {
    this.getPages()
  },
  data() {
    return {
      activePage: 0,
      pages: []
    }
  }, 
  methods: {
    async getPages() {
      let res = await fetch('pages.json')
      let data = await res.json()

      return this.pages = data
    }, 
    pageCreated(pageObj) {
      console.log(pageObj)
      this.pages.push(pageObj)
    }
  }
}
</script>

