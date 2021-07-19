<template>
  <footer class="footer">
    <div class="footer__copyright d-flex justify-content-center">
      <p>{{ year }} | &copy; ZPT Digital </p>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer",
  data () {
    return {
      year: new Date().getFullYear()
    }
  }
};
</script>

<style>
</style>