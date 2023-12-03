<template>
  <div class="background-mask"/>
  <img src="./assets/title.png"  alt="抽奖环节" class="title-pic"/>
    <div class="selected-num">
      <p v-for="num in selected_num" style="
      width: 150px;
      font-size: 100px;
      font-weight: bold;
      text-align: center;
">{{num}}</p>
    </div>
  <button class="raffle-button" @click="onButtonClick">{{!isRaffling ? '开始抽奖' : '结束抽奖'}}</button>


</template>

<script setup>
import {ref, watch, watchEffect} from "vue";
let isRaffling = ref(false)
let nums = []
let selected_num = ref([])
for (let i = 1; i <= 36; i++) {
    nums.push(i)
}
for (let i = 1; i <= 36; i++) {
    nums.push(i)
}
function randomNum() {
    let rand_num = Math.floor(Math.random() * nums.length);
    console.log(nums[rand_num])
    return nums.splice(rand_num, 1)
}

function onButtonClick() {
    isRaffling.value = !isRaffling.value
    if(isRaffling.value) {
        startRaffle();
    }else{
        clearInterval(timer.value)
        for(let i=0; i<5; i++) {
            selected_num.value[i] = randomNum()[0]
        }
    }
}
let timer = ref(null)
function startRaffle() {
   timer.value = setInterval(() => {
       for(let i=0; i<5; i++) {
        selected_num.value[i] = Math.floor(Math.random() * 36) + 1;
       }
    }, 100)
}



</script>

<style scoped>
.background-mask {
    width: 100%;
    height: 100%;
    opacity: 20%;
    background-color: white;
    position: fixed;
    z-index: -1;
}
.title-pic {
    position: absolute;
    top: 15%;
    left: calc(50% - 320px);
}
.raffle-button {
    position: absolute;
    top: 80%;
    left: calc(50% - 100px);
    width: 220px;
    height: 80px;
    border-radius: 10px;
    background-color: #f6da4b;
    border: none;
    font-size: 30px;
    font-weight: bold;
    cursor: pointer;
}
.selected-num {
    position: absolute;
    top: 30%;
    left: calc(50% - 360px);
    cursor: pointer;
    display: flex;
}
</style>
