<template>
  <q-page>
    <div>
      Hello
    </div>
  </q-page>
</template>

<script>
let loaded = false
let loading = false
export default {
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
    },
    async loadWidget () {
      if (loading) {
        return
      }
      if (loaded) {
        return this.createWidget()
      }
      window.__be = window.__be || {}
      window.__be.id = '5d0b3f5296cf0ed8199f4ab1'
      window.BE_API = window.BE_API || {}
      window.BE_API.onBeforeLoad = () => {
        this.createWidget()
        return false
      }
      loading = true
      loaded = await this.loadScript('https://cdn.chatbot.com/widget/plugin.js')
      loading = false
    },
    createWidget () {
      window.BE_API.onLoad = () => {
        if (window.BE_API.isChatClosed()) {
          window.BE_API.openChat()
        }
      }
      window.BE_API.create()
    },
    destroyWidget () {
      if (loaded && window.BE_API.isInitialized()) {
        window.BE_API.destroy()
      }
    }
  },
  created () {
    this.loadWidget()
  },
  beforeDestroy () {
    this.destroyWidget()
  }
}
</script>
