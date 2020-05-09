<template>
  <div class="container">
    <b-row class="mt-5" v-if="!images.length">
      <b-col>
        <b-spinner label="Loading images" variant="primary"></b-spinner>
      </b-col>
    </b-row>
    <div class="gallery">
      <masonry
        :cols="{ default: 5, 1000: 4, 700: 3, 400: 2 }"
        :gutter="{ default: '20px', 700: '10px' }"
      >
        <div v-for="image in images" :key="image.id">
          <img
            :src="image.url"
            :key="image.id"
            :alt="`Image of ${image.name} meme`"
            class="meme-thumb"
            v-b-modal.modal-1
            @click="imgToEdit = image.url"
          />
        </div>
      </masonry>
    </div>

    <b-modal id="modal-1" title="Create your meme">
      <Editor :imgToEdit="imgToEdit" />
    </b-modal>
  </div>
</template>
<script>
import Editor from "@/components/Editor.vue";
export default {
  name: "Gallery",
  components: { Editor },
  data() {
    return {
      images: [],
      imgToEdit: ""
    };
  },
  created() {
    fetch("https://api.imgflip.com/get_memes")
      .then(response => response.json())
      .then(response => (this.images = response.data.memes))
      .catch(err => console.log(err));
  }
};
</script>

<style>
.modal-content {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 100%;
  pointer-events: auto;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 0.3rem;
  outline: 0;
  background: lightgrey !important;
}
</style>
