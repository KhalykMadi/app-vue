<template>
  <div class="container column">
    <ResumeForm @block-added="addBlock" />
    <ResumeView :blocks="blocks" />
  </div>
  <div class="container">
    <AppLoader v-if="loading" />
    <ResumeComments
        v-else
        :comments="comments"
        @load-comments="loadComments"
    />
  </div>
</template>

<script>
import ResumeView from './components/ResumeView.vue'
import ResumeForm from './components/ResumeForm'
import ResumeComments from './components/ResumeComments'
import AppLoader from './components/AppLoader'
export default {
  data() {
    return {
      blocks: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    async loadComments() {
      this.loading = true
      const res = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = await res.json()
      this.loading = false
    },
    addBlock(block) {
      this.blocks.push(block)
    }
  },
  components: {
    ResumeForm, ResumeComments, AppLoader,ResumeView
  }
}
</script>

