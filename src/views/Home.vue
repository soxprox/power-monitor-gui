<template>
  <div class="home">
    <KWHDial />
  </div>
</template>

<script>
import KWHDial from "@/components/KWHDial.vue"
export default {
  name: "Home",
  components: {
    KWHDial
  }

};
</script>

<style scoped>
  .home {
    /* align-items: center; */
    margin-left: 0px;
    margin-right: auto;
    width: 1vh;
  }
</style>
