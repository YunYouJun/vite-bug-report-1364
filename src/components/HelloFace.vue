<template>
  <div style="position: relative" class="margin">
    <img id="demo-img" src="bbt1.jpg" />
    <canvas id="overlay" />
  </div>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
import * as faceapi from "face-api.js";

export default defineComponent({
  name: "HelloFace",
  setup: () => {
    const count = ref(0);
    return { count };
  },

  async mounted() {
    const inputImgEl = document.getElementById("demo-img");
    const canvas = document.getElementById("overlay");

    await faceapi.nets.ssdMobilenetv1.loadFromUri("/models");
    // await faceapi.nets.ssdMobilenetv1.loadFromUri("/models-with-ext");
    const results = await faceapi.detectAllFaces(inputImgEl as any);

    faceapi.matchDimensions(canvas as any, inputImgEl as any);
    faceapi.draw.drawDetections(
      canvas as any,
      faceapi.resizeResults(results, inputImgEl as any)
    );
  },
});
</script>

<style scoped>
#demo-img {
  height: 80vh;
}

.margin {
  display: inline-block;
  margin: 0 auto;
  text-align: center;
}

#overlay,
.overlay {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
