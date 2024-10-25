<script setup>
const props = defineProps(['imgSrc']);
</script>

<template>
  <div id="white-outside">
    <img :src="imgSrc" id="big-image"/>
    <img :src="imgSrc" id="small-image"/>
  </div>
</template>

<style scoped>
#white-outside {
  background-color: white;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.15);
  border-radius: 12px;
  height: 80%;
  aspect-ratio: 3 / 2;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: -3;
}

#big-image {
  filter: blur(10px);
  max-height: 85%;
  max-width: 85%;
}

#small-image {
  max-height: 70%;
  max-width: 60%;
  position: absolute;
}

@media (max-width: 600px) {
  #white-outside {
    width: 90%;
    height: auto;
  }
  #big-image {
    filter: blur(5px);
  }
}
@media (min-width: 601px) and (max-width: 768px) {
  #white-outside {
    width: 90%;
    height: auto;
  }
  #big-image {
    filter: blur(5px);
  }
}
@media (min-width: 769px) and (max-width: 900px) {
  #white-outside {
    width: 90%;
    height: auto;
  }
}
@media (min-width: 901px) and (max-width: 1024px) {
  #white-outside {
    width: 90%;
    height: auto;
    max-width: 60%;
  }
}
@media (min-width: 1025px) {
  #white-outside {
    max-width: 60%;
  }
}
</style>