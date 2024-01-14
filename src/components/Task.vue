<script setup>
import {ref} from "vue";

const tasks = ref([
  {
    'name': 'Task 1',
    'desc' : 'Here are the biggest enterprise technology acquisitions of 2021 so far',
    'time': 1
  },
  {
    'name': 'Task 2',
    'desc' : 'Because it\'s about motivating the doers. Because I\'m here to follow my dreams',
    'time': 75
  }
]);

const popup = ref(false)

const inputs = {
  name: "",
  desc: "",
  time: ""
}
const allData = ref(inputs)
function addNewTask(){
  tasks.value.push(allData.value)
  allData.value = inputs

  popup.value = false
}

function removeTask(index){
  tasks.value.splice(index, 1)
}


</script>

<template>
  <div class="container mx-auto my-5">
    <button @click="popup = !popup" class="inline-flex items-center px-5 py-3 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:outline-none dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add New Task</button>

    <div :class=" popup ? 'show' : 'hidden' " class=" overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
      <div class="relative p-4 w-full max-w-2xl max-h-full m-auto mt-20">
        <!-- Modal content -->
        <div class="relative p-3 bg-white rounded-lg shadow dark:bg-gray-700">
          <!-- Modal header -->
          <div class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600">
            <h3 class="text-xl font-semibold text-gray-900 dark:text-white">
              Add New Task
            </h3>
            <button @click="popup = !popup" type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-hide="static-modal">
              <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 14">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6"/>
              </svg>
              <span class="sr-only">Close modal</span>
            </button>
          </div>
          <!-- Modal body -->
          <form @submit.prevent="addNewTask()" class="px-5 pt-6 pb-2">
            <div class="mb-4">
              <label class="block text-white text-sm font-bold mb-2" for="name">
                Name
              </label>
              <input v-model="allData.name" class="bg-gray-600 shadow appearance-none border border-gray-400 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline" id="name" type="text">
            </div>
            <div class="mb-4">
              <label class="block text-white text-sm font-bold mb-2" for="desc">
                Description
              </label>
              <textarea v-model="allData.desc" class="bg-gray-600 shadow appearance-none border border-gray-400 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline" id="desc" ></textarea>
            </div>
            <div class="mb-4">
              <label class="block text-white text-sm font-bold mb-2" for="name">
                Time
              </label>
              <input v-model="allData.time" class="bg-gray-600 shadow appearance-none border border-gray-400 rounded w-full py-2 px-3 text-white leading-tight focus:outline-none focus:shadow-outline" id="time" type="number">
            </div>

            <!-- Modal footer -->
            <div class="flex items-center p-4 md:p-5 border-t border-gray-200 rounded-b dark:border-gray-600">
              <button type="submit" class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none  font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add Task</button>
              <button @click="popup = !popup" type="button" class="ms-3 text-gray-500 bg-white hover:bg-gray-100 focus:outline-none rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-600">Close</button>
            </div>
          </form>

        </div>
      </div>
    </div>
  </div>

  <div class="tasks container mx-auto pt-5 grid grid-cols-4 gap-4">

    <div v-for="(task, index) in tasks" :key="index" class="max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700">
      <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"> {{ task.name }} </h5>
      <p class="mb-3 font-normal text-gray-700 dark:text-gray-400"> {{ task.desc }} </p>
      <h5 class="mb-2 text-1xl italic tracking-tight text-gray-900 dark:text-white"> Time: {{ task.time }} minute{{ task.time > 1 ? 's' : '' }} </h5>
      <button @click="removeTask(index)" class="mt-4 inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-red-700 rounded-lg hover:bg-red-800 focus:outline-none dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800">
        Remove Task
        <svg class="w-[13px] h-[13px] fill-[#fff] mx-1 my-1" viewBox="0 0 448 512" xmlns="http://www.w3.org/2000/svg">
          <path d="M163.8 0H284.2c12.1 0 23.2 6.8 28.6 17.7L320 32h96c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 96 0 81.7 0 64S14.3 32 32 32h96l7.2-14.3C140.6 6.8 151.7 0 163.8 0zM32 128H416L394.8 467c-1.6 25.3-22.6 45-47.9 45H101.1c-25.3 0-46.3-19.7-47.9-45L32 128zm192 64c-6.4 0-12.5 2.5-17 7l-80 80c-9.4 9.4-9.4 24.6 0 33.9s24.6 9.4 33.9 0l39-39V408c0 13.3 10.7 24 24 24s24-10.7 24-24V273.9l39 39c9.4 9.4 24.6 9.4 33.9 0s9.4-24.6 0-33.9l-80-80c-4.5-4.5-10.6-7-17-7z"></path>

        </svg>
      </button>
    </div>

</div>

</template>

<style scoped>

</style>