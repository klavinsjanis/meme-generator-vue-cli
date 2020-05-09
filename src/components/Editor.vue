<template>
  <div class="editor">
    <div id="downloadImage" ref="downloadImage" :idCanvas="idCanvas">
      <img :src="imgToEdit" :alt="`Image to edit`" :parent="true" id="img" />
      <vue-draggable-resizable :w="60" :h="60" @dragging="onDrag" @resizing="onResize">
        <p id="meme-text">{{topText}}</p>
      </vue-draggable-resizable>
      <vue-draggable-resizable :w="60" :h="60" @dragging="onDrag" @resizing="onResize">
        <p id="meme-text">{{bottomText}}</p>
      </vue-draggable-resizable>
    </div>
    <b-form>
      <p class="modal-info-text">DRAG AND DROP TEXT</p>
      <p class="modal-top-text">Input first text</p>
      <b-input id="text-part-one" class="text-input-meme" v-model="topText" placeholder="Top Text"></b-input>
      <p class="modal-bottom-text">Input second text</p>
      <b-input
        id="text-part-two"
        class="text-inputTwo-meme"
        v-model="bottomText"
        placeholder="Bottom Text"
      ></b-input>
      <b-button @click="downloadImage" class="download-button">Download</b-button>
    </b-form>
  </div>
</template>

<script>
import { saveAsPng } from "save-html-as-image";
import Vue from "vue";
import VueDraggableResizable from "vue-draggable-resizable";
import "vue-draggable-resizable/dist/VueDraggableResizable.css";
Vue.component("vue-draggable-resizable", VueDraggableResizable);

export default {
  name: "Editor",
  props: {
    imgToEdit: {
      type: String
    }
  },
  data() {
    return {
      topText: "",
      bottomText: "",
      width: 0,
      heigth: 0,
      x: 0,
      y: 0,
      idCanvas: "image",
      selectedColor: null,
      selectedFont: null
    };
  },
  methods: {
    downloadImage: function() {
      const node = this.$refs.downloadImage;
      saveAsPng(node, { filename: "new-meme" });
    },
    onResize: function(x, y, width, heigth) {
      this.x = x;
      this.y = x;
      this.width = width;
      this.heigth = heigth;
    },
    onDrag: function(x, y) {
      this.x = x;
      this.y = y;
    },
    mySize: function() {
      this.textSize = self.rng1.value;
    }
  }
};
</script>

<style>
.btn {
  color: #fff;
  background-color: rgb(23, 139, 160) !important;
  border-color: #6c757d;
  float: right;
  margin-top: 20px;
}

.paragraph-top {
  margin-top: 10px;
}

.modal-top-text {
  margin-top: 10px;
  margin-bottom: -3px;
}
.modal-bottom-text {
  margin-top: 10px;
  margin-bottom: -3px;
}

#meme-text {
  color: white !important;
  font-weight: bold;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 36px;
}

.first-slider {
  margin-top: 10px;
}
.vdr {
  border: none;
}
</style>

