<template>
  <div class="page">
    <nav ref="dockRef" class="dock">
      <ul>
        <li
          class="app"
          @mousemove="handleAppHover"
          v-for="index in 7"
          :key="index"
        >
          <a href="https://www.frontend.fyi" target="_blank">
            <img
              src="https://www.frontend.fyi/playground-assets/macos-dock/icons/arc.png"
            />
            <span class="tooltip">Arc Browser</span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import "./index.css";
import { ref } from "vue";
import { scaleValue } from "./utils/scale";

const maxAdditionalSize = 5;

export default {
  setup() {
    const dockRef = ref(null);
    console.log("dockRef: ", dockRef);

    const handleAppHover = (ev) => {
      if (!dockRef.value) return;

      const mousePosition = ev.clientY;
      const iconPositionTop = ev.currentTarget.getBoundingClientRect().top;
      const iconHeight = ev.currentTarget.getBoundingClientRect().height;

      const cursorDistance = (mousePosition - iconPositionTop) / iconHeight;
      const offsetPixels = scaleValue(
        cursorDistance,
        [0, 1],
        [maxAdditionalSize * -1, maxAdditionalSize]
      );

      dockRef.value.style.setProperty(
        "--dock-offset-top",
        `${offsetPixels * -1}px`
      );

      dockRef.value.style.setProperty(
        "--dock-offset-bottom",
        `${offsetPixels}px`
      );
    };
    return {
      dockRef,
      handleAppHover,
    };
  },
};
</script>
