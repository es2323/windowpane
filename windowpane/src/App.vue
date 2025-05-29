<script>
import SiteHeader from './components/SiteHeader.vue'; // Make sure the path is correct

export default {
  name: 'App',
  components: {
    SiteHeader // Register the component
  }
}
</script>

<template>
  <div id="app">
    <SiteHeader />
    <main>
      <h2>Welcome to my portfolio!</h2>
    </main>
  </div>
</template>