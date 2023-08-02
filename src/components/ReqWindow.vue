<template >
  <section class="req-window">
    <div class="req-window__title">Расчёт стоимости проекта</div>
    <div class="req-window__inputs">
      <div class="req-window__inputs_item">
        <div>Площадь</div>
        <input type="number" v-model="square" placeholder="100 м2"> 
      </div>
      <div class="req-window__input_item">
        <div>Название</div>
        <input type="text" placeholder="монтаж кабеля ЭОМ на потолке" v-model="name">
      </div>
      <div class="req-window__input_item">
        <div>Объем материалов процесса</div>
        <input type="text" placeholder="монтаж кабеля ЭОМ на потолке" v-model="processValue">
      </div>
    </div>
    <button @click="sendReq">Расчитать</button>
    <textarea :value="response?.predicted_hours ?? '' + ' ' + response?.predicted_price ?? ''"></textarea>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

const square = ref<number>(0)
const name = ref<string>('')
const processValue = ref<number>(0)
const response = ref<IResponse | null>(null)

interface IRequest{
  Object_area: number
  Process_volume: number
  name: string
}

interface IResponse{
  predicted_hours: string
  predicted_price: string
}

const sendReq = async () => {
  const sendingData: IRequest = {
    Object_area: square.value,
    Process_volume: processValue.value,
    name: name.value
  }

  const { data }= await axios.post<IResponse>('http://localhost:5000/predict', sendingData)
  response.value = data
}

</script>

<style scoped lang="scss">
.req-window{
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3rem;
  font-size: 18px;
  &__title{
    margin-top: 2rem;
    font-size: 20px;
    @media (min-width: 1921px) {
      font-size: 1vw;
      margin-top: 1.6vw ;
    }
  }
  &__inputs{
    display: flex;
    flex-direction: row;
    gap: 3rem;
    @media (min-width: 1921px) {
      gap: 2.4vw;
    }
  }
  @media (min-width: 1921px) {
    font-size: 0.9vw;
  }
  input{
    padding: 8px 16px;
    border-radius: 8px;
    background-color: transparent;
    border: 1px solid $colorBlue;
    outline: none;
    width: 160px;
    @media (min-width: 1921px) {
      width: 8vw;
    }
  }
  textarea{
    padding: 8px 16px;
    border-radius: 8px;
    background-color: transparent;
    border: 1px solid $colorBlue;
    outline: none;
    max-lines: 4;
    width: 240px;
    height: 80px;
    @media (min-width: 1921px) {
      width: 12vw;
      height: 4vw;
    }
  }
}
</style>
