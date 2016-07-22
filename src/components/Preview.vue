<template>
  <webview :src="url" v-el="webview"></webview>
</template>

<script>
  export default {
    props: {
      url: 'String'
    }
  }
</script>
