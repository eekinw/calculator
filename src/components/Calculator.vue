<script setup>

const buttons = [
  "0","1", "2", "3", "4", "5", "6", "7", "8", "9", "+", "-", "=", "÷", "C", "*" 
]

import {ref} from "vue"


const inputValue = ref("")


function handleButtonClick(button) {
  // if C is pressed, reset value 
  if( button === "C") {
    inputValue.value = ""
  } else if ( button === "=") {
    if(inputValue.value.includes("+")) {
      addValue()
    } else if(inputValue.value.includes("-")) {
      subtractValue()
    } else if (inputValue.value.includes("*")) {
      productValue();
    } else if (inputValue.value.includes("÷")) {
      divideValue();
    }
  } else {
    inputValue.value += button
  }
}

function addValue() {
  const numbers = inputValue.value.split("+")
  const sum = numbers.reduce((accumulator, value) => Number(accumulator) + Number(value),0)

  inputValue.value = sum
}

function subtractValue() {
  const numbers = inputValue.value.split("-")
  const subtract = numbers.reduce((accumulator, value) => Number(accumulator) - Number(value))

  inputValue.value = subtract
  
}

function productValue() {
  const numbers = inputValue.value.split("*")
  const multiply = numbers.reduce((accumulator, value) => Number(accumulator) * Number(value), 1)

  inputValue.value = multiply
}

function divideValue() {
    const numbers = inputValue.value.split("÷")
    const divide = numbers.reduce((accumulator, value) => Number(accumulator) / Number(value))

  inputValue.value = divide
  
}

</script>


<template>
<div class="lg:w-2/5 bg-white m-auto max-h-2/5 min-w-3/5 rounded-lg p-5 border-solid border-2 border-teal-800">
  
  <div class="flex flex-wrap justify-center gap-5">
    <input v-model="inputValue" class="text-4xl font-bold px-3 py-1 rounded-lg text-center" type="text">
  </div>

  <div class="grid grid-rows-4 grid-flow-col gap-1 border-solid border-3 border-black">
    <button v-for="(button, index) in buttons"
    :key="index"
    class="bg-[#e5e7eb] mt-7 w-auto rounded-md active:bg-yellow-300"
    @click="handleButtonClick(button)"
    >
    {{ button }}
    </button>
  </div>
  </div>
    
</template>