<template>
  <div class="home">
    <Gallery />
  </div>
</template>

<script>
// @ is an alias to /src
import Gallery from "@/components/Gallery.vue";

export default {
  name: "Home",
  components: {
    Gallery,
  },
};
</script>

<style>
body {
  background-color: salmon !important;
}
img {
  display: block;
  width: 100%;
  margin-top: 5px;
  border: 2px solid #021a40 !important;

}
</style>
