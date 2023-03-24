<template>
  <div class="svg-wrapper">
    <Drawing></Drawing>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useAppStore } from "@/store/app";

// import HelloWorld from "@/components/HelloWorld";
import { SVG } from "@svgdotjs/svg.js";
import Drawing from "@/components/Drawing";

const store = useAppStore();
const foreignObject = ref(null);
// const mainSvg = ref(null);

onMounted(() => {
  store.svg = SVG("#my-svg");
});
</script>

<style>
.svg-wrapper {
  background: pink;
  width: 100%;
  height: 100%;
}

.main-svg {
  width: 100%;
  height: 100%;
}
</style>
