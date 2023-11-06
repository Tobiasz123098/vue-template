<template>
  <div id="main-container" class="container mb-3">
    <form id="form-container" class="col">
      <div class="col mb-3">
        <label for="" class="form-label">
          Page Title
        </label>
        <input 
          type="text" 
          class="form-control"
          v-model="pageTitle"
        />
      </div>
      <div class="mb-3">
        <label for="" class="form-label">
          Content
        </label>
        <textarea 
          type="text" 
          class="form-control" 
          rows=5
          v-model="content"
        >
        </textarea>
      </div>
      <div class="mb-3">
        <button 
          class="btn btn-primary"
          :disabled="isFormInvalid"
          @click.prevent="submitForm"
        >
          Create Page
        </button>
      </div>
    </form>
    <div 
      id="link-container" 
      class="col"
    >
      <div class="mb-3">
        <label for="" class="form-label">
          Link Text
        </label>
        <input 
          type="text" 
          class="form-control"
          v-model="linkText"
        />
      </div>
      <div class="mb-3">
        <label for="" class="form-label">
          Link URL
        </label>
        <input 
          type="text" 
          class="form-control"
          v-model="linkUrl"
        />
      </div>
      <div class="form-check">
        <input class="form-check-input" type="checkbox" value="">
        <label class="form-check-label" for="flexCheckDefault">
          Published
        </label>
      </div>
    </div>

  </div>
</template>
<script>

export default {
  props: ['pageCreated'], 
  data() {
    return {
      pageTitle: '', 
      content: '', 
      linkText: '', 
      linkUrl: ''
    }
  }, 
  computed: {
    isFormInvalid() {
      return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl
    }
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) 
        alert('Please fill the form')

      this.pageCreated({
        pageTitle: this.pageTitle,
        content: this.content,
        link: {
          text: this.linkText, 
          url: this.linkUrl
        } 
      })
    }
  }
}
</script>
<style scoped>
  #main-container {
    display: flex;
    margin-top: 25px;
  }

  #form-container {
    padding: 8px;
  }

  #link-container {
    padding: 8px;
  }
</style>
