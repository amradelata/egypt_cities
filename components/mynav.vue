<template>
  <div>
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <nuxt-link to="/" class="navbar-item" href="https://bulma.io">
          <img src="https://i.ibb.co/P57NMVc/egypt.png" />
        </nuxt-link>

        <a
          @click="togelphonemenu()"
          role="button"
          class="navbar-burger burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarBasicExample"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div id="navbarBasicExample" class="navbar-menu" ref="phonemenu">
        <div class="navbar-start">
          <nuxt-link to="/about" class="navbar-item">About</nuxt-link>

          <nuxt-link to="/govers" class="navbar-item">Egypt cities</nuxt-link>
          <nuxt-link to="/admin" class="navbar-item">controls</nuxt-link>
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a class="button is-primary" href="https://www.patreon.com/user?u=25798954">
                <strong>patreon</strong>
              </a>
              <a class="button is-light" href="https://www.amradelata.com/">My website</a>
            </div>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>
  

<script>
export default {
  methods: {
    togelphonemenu() {
      this.$refs["phonemenu"].classList.toggle("navbar-menu");
    }
  }
};
</script>

<style  scoped>
@media screen and (max-width: 768px) {
  .navbar-item,
  .navbar-link {
    text-align: center;
  }
  .buttons {
    justify-content: center;
  }
}
</style>