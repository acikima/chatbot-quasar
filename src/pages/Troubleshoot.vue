<template>
  <q-page>
    <div>
      Hello

    </div>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
    }
  },
  mounted () {
    window.BE_API.create()

    window.BE_API.onLoad = () =>
      window.BE_API.openChat()
  },
  created () {

  },
  methods: {

  },
  beforeDestroy () {
    console.log('before destroy')
    window.BE_API.destroy()
  }

}
</script>

<style>
</style>
