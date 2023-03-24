<template>
  <v-container class="fill-height">
    <div class="wrapper">
      <!-- <Drawing></Drawing> -->
      <!-- <InlineSvg id="my-svg"></InlineSvg> -->
      <!-- <svg id="my-svg" :src="MySVG" alt="Your SVG"></svg> -->
      <MySVG id="my-svg"></MySVG>
    </div>
    <Teleport v-if="svgHasMounted" to=".circle1-inject">
      <div
        xmlns="http://www.w3.org/1999/xhtml"
        style="
          position: relative;
          overflow: auto;
          font-family: Arial;
          font-weight: 400;
          font-size: 12px;
          line-height: 100%;
        "
      >
        Yoyo
        <div class="hello-world">Hello World</div>
        <span class="copy-popover">Click to Copy</span>
      </div>
    </Teleport>
  </v-container>
</template>

<script setup>
import { onMounted, nextTick, ref, watchEffect } from "vue";
import InlineSvg from "vue-inline-svg";
// import Drawing from "@/components/Drawing";
import MySVG from "@/assets/Drawing.svg";
import HelloWorld from "@/components/HelloWorld";

import {
  SVG,
  extend as SVGextend,
  Element as SVGElement,
} from "@svgdotjs/svg.js";
const svgHasMounted = ref(false);
const convertBBoxToViewBox = (bbox) => {
  const { x, y, w, h } = bbox;
  // const [xMin, xMax, width, heigt] = viewBox;
  return [x, y, w, h];
};

watchEffect(() => {
  console.log(
    "🚀 ~ file: SvgWrapper.vue:28 ~ svgHasMounted:",
    svgHasMounted.value
  );
});

onMounted(() => {
  const draw = SVG("#my-svg").viewbox(0, 0, 800, 800).addTo(".wrapper");
  const rect = draw.rect(100, 100).attr({ fill: "#f06" });
  const drawBBox = draw.bbox();
  const viewsGroup = draw.find(".main-group");
  const circle1 = draw.findOne(".circle-1");
  const circle2 = draw.findOne(".circle-2");
  const circle3 = draw.findOne(".circle-3");
  const viewBox = convertBBoxToViewBox(circle1.bbox());
  // draw.animate({ duration: 2000, delay: 1000 }).viewbox(...viewBox);

  var foreignObject = viewsGroup
    .foreignObject()
    .addClass("circle1-inject")
    .attr({
      width: circle1.bbox().width,
      height: circle1.bbox().height,
      x: circle1.bbox().x,
      y: circle1.bbox().y,
    });

  svgHasMounted.value = true;
});
</script>
<style>
.wrapper {
  border: 2px dotted #f06;
  width: 100%;
  height: 100%;
}

#my-svg {
  width: 100%;
  height: 100%;
}
</style>
