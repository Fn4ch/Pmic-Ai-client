<template >
  <div class="calculation" v-if="!isCalculated" @click="log">
    <section class="calculation__window">
      <div class="req-form">
        <h1>Прогноз затрат</h1>
        <h4>Введите исходные данные для запроса</h4>
          <select v-model="name" placeholder="Монтаж кабеля ЭОМ на потолке">
            <option value="" disabled selected>Выберите процесс</option>
            <option v-for="option in options" :key="option" :value="option" class="option">{{ option }}</option>
          </select>
            <input type="number" v-model="square" placeholder="Введите длину, м2"> 
        <button @click="sendReq">Расчитать</button>
      </div>
    </section>
  </div>
  <div class="calculated" v-else>
    <div class="calculated__result">
      <h1>Прогнозируемые параметры</h1>
      <div class="calculated__values">
        <div class="calculated__item">
          <div class="calculated__item_title">
            Длительность процесса
          </div>
          <div class="calculated__item-value" v-if="response?.predicted_hours">
            {{ response?.predicted_hours }}
          </div>
          <Loader v-else/>
        </div>
        <div class="calculated__item">
          <div class="calculated__item_title">
            Затраты на процесс
          </div>
          <div class="calculated__item-value" v-if="response?.predicted_price">
            {{ response?.predicted_price }}
          </div>
          <Loader v-else/>
        </div>
      </div>
    </div>
    <ObjectSvg class="calculated__img"/>
  </div>
</template>

<script setup lang="ts">
import ObjectSvg from './ObjectSvg.vue'
import { ref } from 'vue'
import axios from 'axios'
import Loader from './Loader.vue';

const square = ref<number | null>(null)
const name = ref<string>('')
const response = ref<IResponse | null>(null)

const isCalculated = ref<boolean>(false)

function log() {
  console.log(name.value)
}

const options: string[] = [
  'Кабель ЭОМ пол',
  'Лобики ГКЛ',
  'Мариофф (основной объем)',
  'ОВ2 (воздуховоды)',
  'Фальшпол (+обеспыливание)',
  'Монтаж кабеля ЭОМ на потолке'
]


interface IResponse{
  predicted_hours: string
  predicted_price: string
}

const customConfig = {
    headers: {
    'Content-Type': 'application/json'
    }
}

const sendReq = async () => {
  const sendingData = {
    Object_area: square.value,
    "Название процесса": name.value
  }

  try {
    isCalculated.value = true
    const { data } = await axios.post<IResponse>('http://localhost:5000/predict', sendingData, customConfig)
    response.value = data
  }
  catch (e) {
    alert(e)
    return
  }
}

</script>

<style scoped lang="scss">
.calculated{
  align-self: center;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 80px;
  width: 100vw;
  padding: 0 48px;
  margin-bottom: 10vh;
  @media (min-width: 1921px) {
    gap: 4vw;
    padding: 0 2.4vw;
  }
  @media (max-width: 1024px) {
    padding: 0 24px;
    flex-direction: column;
  }
  &__result{
    display: flex;
    flex-direction: column;
    gap: 64px;
    @media (min-width: 1921px) {
      gap: 3.2vw;
    }
  }
  &__values{
    display: flex;
    gap: 32px;
    @media (min-width: 1921px) {
      gap: 1.6vw;
    }
  }
  &__item{
    display: flex;
    flex-direction: column;
    gap: 48px;
    @media (min-width: 1921px) {
      gap: 2.4vw;
    }
    &_title{
      font-size: 16px;
      color: $colorGrey;
      @media (min-width: 1921px) {
        font-size: .8vw;
      }
    }
  }
  &__item-value{
    font-size: 64px;
    line-height: 1.2;
    @media (min-width: 1921px) {
      font-size: 3.2vw;
    }
  }
  &__img{
    z-index: 10;
  }
}
.calculation{
  align-self: center;
  display: flex;
  justify-content: center;
  background-color: $colorBlueLight;
  width: 100vw;
  height: min-content;
  margin-bottom: 8vh;
  @media (max-width: 300px) {
    width: 100%;
  }

  &__window{
    margin: 56px;
    width: 50vw;
    background-color: $colorWhite;
    z-index: 5;
    @media (max-width: 1024px) {
      margin: 56px 0;
      width: 70vw;
    }
    @media (max-width: 768px) {
      margin: 56px auto;
      width: auto;
    }
  }
}
h1{
  font-size: 48px;
  font-weight: 400;
  @media (min-width: 1921px) {
    font-size: 2.4vw;
  }
  @media (max-width: 768px) {
    font-size: 32px;
  }
}
h4{
  font-size: 20px;
  font-weight: 400;
  @media (min-width: 1921px) {
    font-size: 1vw;
  }
   @media (max-width: 768px) {
    font-size: 15px;
  }
}
.req-form{
  margin: 48px 72px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 24px;
  font-size: 18px;
  width: min-content;
  background-color: $colorWhite;
  @media (min-width: 1921px) {
    margin: 2.4vw 3.6vw ;
    font-size: 0.9vw;
    gap: 1.2vw;
    font-size: .9vw;
  }
  @media (max-width: 768px) {
    margin: 12px 20px;
  }
  input, select{
    padding: 12px 0px;
    background-color: transparent;
    border: none;
    border-bottom: 1px solid $colorBlack;
    outline: none;
    width: 500px;
    @media (max-width: 1440px) {
      width: 400px;
    }
    @media (max-width: 768px) {
      width: 300px;
    }
    @media (max-width: 440px) {
      width: 240px;
    }
    font-size: 16px;
    @media (min-width: 1921px) {
      width: 25vw;
      padding: 0.6vw 0vw;
      font-size: 0.8vw;
    }
  }
}
button{
  align-self: flex-end;
  background-color: $colorBlue;
  padding: 10px 40px;
  border-radius: 8px;
  border: none;
  color: $colorWhite;
  font-size: 16px;
  line-height: 18px;
  transition: all 0.2s ease;
  &:active{
    scale: 1.05;
  }
  @media (min-width: 1921px) {
    line-height: .9vw;
    padding: .5vw 2vw;
    font-size: .8vw;
    border-radius: .4vw;
  }
}
.option{
  padding: 8px 12px;
  @media (min-width: 1921px) {
    padding: .4vw .6vw;
  }
}
</style>
