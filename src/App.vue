<template>
<div class="w-full h-screen bg-gray-100 pt-8">

        <div class="bg-white p-3 max-w-md mx-auto">
          <form @submit.prevent="addNewTodo">
            <div class="text-center">
                <h1 class="text-3xl font-bold">ToDo App</h1>
                <div class="mt-4 flex">
                    <input v-model="newTodo" class="w-80 border-b-2 border-gray-500 text-black" type="text" placeholder="Enter your task here" />
                      <button type="submit" class="ml-2 border-2 border-green-500 p-2 text-green-500 hover:text-white hover:bg-green-500 rounded-lg flex">   
                          <PlusIcon class="h-6 w-6 text-green-500"/>
                          <span>Add</span>
                      </button>
                </div>        
            </div>
          </form>
            <div class="mt-8">
                <ul>
                    <li v-for="(todo, index) in todos" :key="todo.index" class="p-2 rounded-lg" >
                        <div class="flex align-middle flex-row justify-between">
                            
                            <div class="p-2">
                                <p @click="todo.finish = !todo.finish" :class="todo.finish ? 'line-through' : null" class="text-lg text-gray-400">{{index}}. {{todo.content}}</p>
                            </div>
                            <button  @click="removeTodo(index)" class="flex text-red-500 border-2 border-red-500 p-2 rounded-lg">
                                <XIcon class="h-6 w-6 text-red-500"/>
                                <span>Remove</span>
                            </button>
                        </div>
                        <small>{{todo.date}}</small>
                        <hr class="mt-2"/>
                    </li>
                </ul>
            </div>
            <div class="mt-8">
                <button @click="markAll" class="border-2 border-red-500 p-2 text-red-500">Completed Task</button>
                <button @click="removeAll" class="border-2 border-indigo-500 p-2 text-indigo-500 ml-4">Remove Todo</button>
            </div>
        </div>    
    </div>
</template>

<script setup>
import {ref} from 'vue'
import { PlusIcon, XIcon } from '@heroicons/vue/outline'
import moment from 'moment'

const newTodo = ref('')
const todos = ref([])
var dateNow = Date.now()
const timeNow = ((value) => moment(value).fromNow())

function addNewTodo(){
  todos.value.push({
    date: timeNow(dateNow),
    content: newTodo.value,
    finish: false
  })
  newTodo.value = ''
}

function markAll(){
  todos.value.forEach((todo) => todo.finish = true);
}

function removeTodo(value){
  todos.value.splice(value, 1)
}
function removeAll(){
  todos.value = []
}


</script>