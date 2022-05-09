<template>
  <div>
    <div
      class="header"
      v-bind:style="classHeader"
    >
    <transition name="fade"
    >
      <img :src="classHeader.src" alt="" />
    </transition>

      <!-- <div class="gradient"></div> -->
    </div>
    <div v-bind:style="{height : 'calc(100vh - 20px)'}" ></div>
  </div>
</template>

<script>
export default {
  name: "HeaderUf",
  props: ["classHeader"],
};
</script>

<style >
@keyframes go {
  from {
    background: #fff;
  }
  to {
    background: #999;
  }
}

.fade-enter-active {
  animation: go 2s;
}
.header * {
  box-sizing: border-box;
}
.header {
  /* border: 10px solid black; */
  width: calc(100% - 20px);
  position: fixed;
  pointer-events: none;
display: block;
}
#header-padding {
    color:red;
  height: calc(100vh - 10px) !important;
  width: 100%;
  position: relative;
}
img {
  object-fit: contain;
  transform-origin: center;
  height: 100%;
  float: left;
}
</style>