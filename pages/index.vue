<script setup lang="ts">
import { ref } from 'vue';

interface ITodo {
    title: string
    status: boolean
    
}

const todos = ref<ITodo[]>([])
const newTodo = ref<string>('')


const addTodo = () => {
    if (newTodo.value.trim() !== ''){
        todos.value.push({ title: newTodo.value, status: false})

        newTodo.value = ''

    }
}    

const removeTodo = (index: number) => {
    todos.value.splice(index, 1)

}

</script>

<template>
    <div class="w-1/2 flex flex-col mx-auto py-4 gap-3">
        <h1 class="text-3xl font-semibold">Daftar Todo</h1>


        <div class="flex gap-2">
            <input v-model="newTodo" class="w-full p-2 border-2 border-blue-400" type="text" placeholder="Tambah Tugas Baru" @keyup.enter="addTodo">
            <button class="p-2 bg-blue-400 text-white" @click="addTodo">Tambah</button>
        </div>
        
        <div class="flex gap-2 justify-between pb-2 border-b-[1px] border-gray-300" 
        v-for="(todo,index) in todos" :key="index"
        >
            <div class="flex gap-2">
                <input v-model="todo.status" type="checkbox">
                <span :class="{'line-through': todo.status}">{{ todo.title }}</span>
            </div>

            <button @click="removeTodo(index)">Hapus</button>
            
        </div>

    </div>
</template>

<style></style>