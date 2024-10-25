<script setup>
import * as AMOL from '@/assets/amol/amol.js';
import { ref, watch } from 'vue';

const props = defineProps(['viewStatus']);

const message = ref("");
const messageTwo = ref(englishVer);

const englishVer = "Tokyo Tower: Visit this iconic landmark for stunning panoramic views of the city. The observation decks provide a great perspective, especially at sunset.";
const chineseVer = "東京鐵塔：參觀這座標誌性地標，欣賞令人驚嘆的城市全景。觀景台提供了絕佳的視野，尤其是在日落時分。";
const englishVer2 = "Mount Aso: Discover this impressive active volcano with its stunning caldera and scenic views. Enjoy hiking trails and relax in nearby hot springs!";
const chineseVer2 = "阿蘇火山：探索這座令人印象深刻的活火山及其令人驚嘆的火山口和風景。享受遠足小徑並在附近的溫泉放鬆！";
let myEffect, myEffect2, btn1, btn2, btn3;
let myScene2, input1, intervalOne;
let myScene3, virtualBtn;

// for Main Scene in Amol.js
function setTokyo() {
    myEffect = AMOL.create('amol-cursor-trail-ripple', 0);
    myEffect2 = AMOL.create('amol-click-tracking-vanilla', 0);

    btn1 = AMOL.create('amol-button-ripple', 1);
    btn1.setScale(1.5);
    btn1.setPosition(-5, 1.5, 0);
    btn1.setListener('click', () => { messageTwo.value = chineseVer; });

    btn2 = AMOL.create('amol-button-ripple', 1);
    btn2.setScale(1.4);
    btn2.setPosition(4.3, -1.5, 0);

    btn3 = AMOL.create('amol-button-thunder', 0);
    btn3.setPosition(-2.2, 2, 0);
}
function deleteCurrent() {
    myEffect.removeSelf();
    myEffect2.removeSelf();
    btn1.removeSelf();
    btn2.removeSelf();
    btn3.removeSelf();
}
function setKumamoto() {
    myEffect = AMOL.create('amol-cursor-trail-ripple', 0);
    myEffect2 = AMOL.create('amol-click-tracking-golden', 1);

    btn1 = AMOL.create('amol-button-golden', 1);
    btn1.setScale(1.2);
    btn1.setPosition(-4.6, 1.5, 0);
    btn1.setListener('click', () => { messageTwo.value = chineseVer2; });

    btn2 = AMOL.create('amol-button-golden', 1);
    btn2.setScale(1.1);
    btn2.setPosition(4.5, -1.5, 0);

    btn3 = AMOL.create('amol-button-golden', 0);
    btn3.setScale(0.7);
    btn3.setPosition(-1.8, 2, 0);
}
setTokyo();
AMOL.animate();

// for Virtual Scene (No.2 Scene) in Amol.js
myScene2 = AMOL.virtualScene(2, 400, 300, 0, 64);
function setTokyo2() {
    input1 = myScene2.create('amol-input-thunder', 0);
    input1.setScale(1.5);
    intervalOne = setInterval(() => { message.value = input1.getValue() }, 200);
}
function deleteCurrent2() {
    input1.removeSelf();
    clearInterval(intervalOne);
}
function setKumamoto2() {
    input1 = myScene2.create('amol-input-thunder', 1);
    input1.setScale(1.5);
    intervalOne = setInterval(() => { message.value = input1.getValue() }, 200);
}
setTokyo2();
myScene2.animate();

// for Virtual Scene (No.3 Scene) in Amol.js
myScene3 = AMOL.virtualScene(2, 400, 400, 50, 8);
function setTokyo3() {
    virtualBtn = myScene3.create('amol-button-ripple', 0);
    virtualBtn.setScale(1.8);
    virtualBtn.setListener('click', () => { messageTwo.value = englishVer; });
}
function deleteCurrent3() {
    virtualBtn.removeSelf();
}
function setKumamoto3() {
    virtualBtn = myScene3.create('amol-button-thunder', 1);
    virtualBtn.setScale(1.8);
    virtualBtn.setListener('click', () => { messageTwo.value = englishVer2; });
}
setTokyo3();
myScene3.animate();

function cleanMemory() {
    deleteCurrent();
    deleteCurrent2();
    deleteCurrent3();
}
function setTokyoScene() {
    setTokyo();
    setTokyo2();
    setTokyo3();
}
function setKumamotoScene() {
    setKumamoto();
    setKumamoto2();
    setKumamoto3();
}
watch(() => props.viewStatus, (newValue) => {
  if (newValue === 'threeView1') {
    AMOL.cameraSpeed(0, 0, -0.15);
    setTimeout(() => {
        AMOL.stopCamera();
        cleanMemory();
        setTokyoScene();
        AMOL.cameraSpeed(0, 0, 0.15);
        messageTwo.value = englishVer;
    }, 2000);
    AMOL.stopCameraAt(0, 0, 20);
  }
  if (newValue === 'threeView2') {
    AMOL.cameraSpeed(0, 0, -0.15);
    setTimeout(() => {
        AMOL.stopCamera();
        cleanMemory();
        setKumamotoScene();
        AMOL.cameraSpeed(0, 0, 0.15);
        messageTwo.value = englishVer2;
    }, 2000);
    AMOL.stopCameraAt(0, 0, 20);
  }
});
</script>

<template>
<div id="white-pad">
    <div id="text1">{{ message }}</div>
</div>

<div id="describe-one">{{ messageTwo }}</div>
</template>

<style scoped>
#white-pad {
    background-color: rgb(255, 255, 255, 0.8);
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.12);
    border-radius: 12px;
    width: 360px;
    height:400px;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    position: absolute;
    left: 65%;
    z-index: -2;
}
#white-pad #text1 {
    background-color: none;
    color: rgb(252, 171, 117);
    width: 80%;
    height: 20%;
    margin: 15%;
    font-weight: bold;
    font-size: 1.5em;
    word-wrap: break-word;
    overflow-wrap: break-word;
    overflow: hidden;
}

#describe-one {
    background-color: rgb(255, 255, 255, 0.8);
    color: rgb(132, 165, 180);
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.12);
    border-radius: 12px;
    width: 360px;
    height:500px;
    padding: 48px;
    font-weight: bold;
    font-size: 1.5em;
    word-wrap: break-word;
    overflow-wrap: break-word;
    overflow: hidden;
    position: absolute;
    bottom: 0%;
    left: 10%;
    z-index: 1;
}

@media (max-width: 600px) {

}
@media (min-width: 601px) and (max-width: 768px) {

}
@media (min-width: 769px) and (max-width: 900px) {

}
@media (min-width: 901px) and (max-width: 1024px) {
  
}
@media (min-width: 1025px) {
  
}
</style>