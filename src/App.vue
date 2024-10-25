<script setup>
import { ref } from 'vue';
import MainImage from './components/MainImage.vue';
import ThreeView from './components/ThreeView.vue';
import japan1 from '@/assets/images/japan1.jpg';
import japan2 from '@/assets/images/japan2.jpg';

const imgSrc = ref(japan1);
const viewStatus = ref("threeView1");
const mainCtrlStyle = ref("opacity: 0;");
const blurAreaStyle = ref("visibility: hidden; opacity: 0;");

const images = [japan1, japan2];
const views = ["threeView1", "threeView2"];
let currentIndex = 0;
const changeView = () => {
  currentIndex = (currentIndex + 1) % images.length;
  setTimeout(() => { imgSrc.value = images[currentIndex]; }, 2000);
  viewStatus.value = views[currentIndex];

  setTimeout(() => { blurAreaStyle.value = "visibility: visible; opacity: 1;"; }, 1900);
  setTimeout(() => { blurAreaStyle.value = "visibility: hidden; opacity: 0;"; }, 2400);
};

const changeThisOpacity = () => { mainCtrlStyle.value = "opacity: 0.9;"};
const resetThisOpacity = () => { mainCtrlStyle.value = "opacity: 0;"};
</script>

<template>
  <div id="app">
    <div id="blur-area" :style="blurAreaStyle"></div>

    <ThreeView :view-status="viewStatus" />
    <div id="main-control" @click="changeView" @mouseover="changeThisOpacity" @mouseout="resetThisOpacity" :style="mainCtrlStyle">Change</div>
    <MainImage :img-src="imgSrc" />
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  overflow: hidden;
}
body::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url('@/assets/images/blue-background.jpg');
  background-size: cover;
  background-position: center;
  opacity: 0.06;
  z-index: -3;
}

#app {
  background-color: none;
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
  position: absolute;
}

#blur-area {
  visibility: hidden;
  background-color: rgba(255, 255, 255, 0.3);
  opacity: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  backdrop-filter: blur(10px);
  z-index: 3;
  transition: 0.5s;
}

#main-control {
  background-color: white;
  color: rgba(128, 128, 128, 0.5);
  opacity: 0;
  cursor: pointer;
  border-radius: 150px;
  position: absolute;
  top: 50%;
  left: 50%;
  width: 250px;
  height: 250px;
  font-weight: bold;
  font-size: 2.5em;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translate(-50%, -50%);
  z-index: 2;
  transition: 0.6s;
}

@media (max-width: 600px) {}
@media (min-width: 601px) and (max-width: 768px) {}
@media (min-width: 769px) and (max-width: 900px) {}
@media (min-width: 901px) and (max-width: 1024px) {}
@media (min-width: 1025px) {}
</style>
