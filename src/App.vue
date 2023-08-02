<template>
  <div class="app" id="app">
    <h1>PmicAi client</h1>
    <ReqWindow />
  </div>
</template>

<script setup lang="ts">
import ReqWindow from './components/ReqWindow.vue';


</script>

<style lang="scss">
#app{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
h1{
    font-size: 2rem;
  @media (min-width: 1921px) {
    font-size: 1.6vw ;
  }
}
button{
  background-color: $colorBlue;
  padding: 8px 16px;
  border-radius: 8px;
  border: none;
  color: $colorWhite;
  transition: all 0.2s ease;
  &:active{
    scale: 1.05;
  }
}
</style>
