<template>
  <footer class="footer bg-dark">
    <div class="container footer-container">
      <div class="d-flex align-items-center justify-content-between footer-items">
        <div class="logo-full">
          <img class="logo-footer" src="@/assets/logo-full.png" />
        </div>
        <div class="left-text text-white d-flex justify-content-end align-items-center">
          <h3>
            Módulo administrativo
          </h3>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style>
.footer {
  height: 120px;
}

.footer-container,
.footer-items {
  height: inherit;
}

.footer-content {
  color: white;
}

.logo-footer {
  width: 200px;
}

.icon-social {
  color: orangered;
}
</style>