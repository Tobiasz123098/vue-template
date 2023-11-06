<template>
  <nav 
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
  >
      <a class="navbar-brand">MyVue</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
      <div v-for="(page, index) in pages" :key="index" 
          class="navbar-nav">
          <navbar-link
            :page="page"
            :isActive="activePage === index"
            @click.prevent="navLinkClick(index)"
          />
      </div>
      </div>
      <form class="d-flex">
      <button 
          class="btn btn-primary" 
          @click.prevent="changeTheme"
      >
          Toggle
      </button>
      </form>
  </nav>
  <page-viewer
    :page="pages[activePage]"
  />
</template>
<script>
import NavbarLink from '@/components/NavbarLink.vue'
export default {
  components: {
    NavbarLink
  },
  created() {
    this.getThemeSetting()
  },
  props: ['pages', 'activePage', 'navLinkClick'],
  data() {
    return {
      theme: 'dark'
    }
  }, 
  methods: {
    changeTheme() {
      let theme = 'light' 
      if (this.theme === 'light') {
        theme = 'dark'
      }
      this.theme = theme
      this.storeThemeSetting()
    }, 
    storeThemeSetting() {
      localStorage.setItem('theme', this.theme)
    }, 
    getThemeSetting() {
      let theme = localStorage.getItem('theme')

      if (theme) {
        this.theme = theme
      }
    }
  }
}
</script>
<style scoped>
  nav {
    padding: 15px;
  }
</style>