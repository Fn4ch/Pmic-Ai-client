<template>
  <div class="app" id="app">
    <PmicLogo />
    <ReqWindow />
  </div>
  <Figures />
</template>

<script setup lang="ts">
import ReqWindow from './components/ReqWindow.vue'
import PmicLogo from './components/PmicLogo.vue'
import Figures from './components/Figures.vue'

</script>

<style lang="scss">
body{
  overflow-x: hidden;
  margin: 0 auto;
  width: 50vw;
  @media (min-width: 1921px) {
    width: 50vw;
  }
  @media (max-width: 1024px) {
    width: 800px;
  }
  @media (max-width: 768px) {
    width: 500px;
  }
  @media (max-width: 440px) {
    width: 300px;
  }
}
.app{
  padding: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  min-height: 100vh;
}
h1{
    font-size: 2rem;
  @media (min-width: 1921px) {
    font-size: 1.6vw ;
  }
}
</style>
