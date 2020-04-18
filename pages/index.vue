<template>
  <div>
    <div class>
      <mynav />
      <hero />
    </div>
    <myfooter />
  </div>
</template>

<script>
import mynav from "~/components/mynav.vue";
import myfooter from "~/components/myfooter.vue";
import hero from "~/components/hero.vue";

export default {
  components: {
    mynav,
    myfooter,
    hero
  }
};
</script>

<style>
</style>
