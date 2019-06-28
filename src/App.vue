<template>
  <div id="q-app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {

    }
  },
  async created () {
    window.__be = window.__be || {}
    window.__be.id = '<YOUR_CLIENT_ID>'
    window.BE_API = window.BE_API || {}
    window.BE_API.onBeforeLoad = () => false

    this.widget = await this.loadScript('https://cdn.chatbot.com/widget/plugin.js')
  },
  methods: {
    loadScript (src) {
      return new Promise(resolve => {
        const script = document.createElement('script')
        script.type = 'text/javascript'
        script.src = src
        script.onload = () => resolve(true)
        script.onerror = () => resolve(false)

        document.head.appendChild(script)
      })
    }
  }
}
</script>

<style>
</style>
