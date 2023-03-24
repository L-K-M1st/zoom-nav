<template>
  <v-card class="resize" style="pointer-events: auto; z-index: 2">
    <v-card-text>
      <v-row>
        <div class="hello-world">Hello World</div>
        <span class="copy-popover">Click to Copy</span>
        <v-btn color="orange" elevation="5" @click.prevent="onButtonClick"
          >Hello Button</v-btn
        >
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script setup>
import { useAppStore } from "@/store/app";
import { storeToRefs } from "pinia";
import { SVG } from "@svgdotjs/svg.js";
// const { svg } = storeToRefs(useAppStore());
const onButtonClick = () => {
  console.log("Hello Button");

  const svg = SVG("#my-svg");
  console.log("🚀 ~ file: HelloWorld.vue:24 ~ onButtonClick ~ svg:", svg);

  const box = svg.findOne("#rect-1");
  const bbox = box.bbox();
  console.log("🚀 ~ file: HelloWorld.vue:29 ~ onButtonClick ~ bbox:", bbox);
  console.log("🚀 ~ file: HelloWorld.vue:28 ~ onButtonClick ~ box:", box);
  svg.animate().viewbox(`${bbox.x} ${bbox.y} ${bbox.width} ${bbox.height}`);
};
</script>

<style>
.hello-world {
  width: 100%;
  height: 100%;
}

.fill-height {
  display: inline-block;
  height: 100%;
}

.resize {
  /* transform: scale(0.4); */
}
</style>
