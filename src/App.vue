<template>
  <div class="container w-[1200px] mx-auto my-4">
    <h1 class="text-3xl text-center font-bold text-indigo-700">ToDo App</h1>
    <div class="flex items-center justify-center gap-10 my-12">
      <input 
      type="text" 
      placeholder="Add new tasks" 
      v-model="inputValue"
      class="border-2 py-3 px-5 w-full outline-amber-500 rounded-lg">
      <button class="btn bg-green-700 text-white font-bold py-3 px-9 rounded-lg"
      @click="addTodo" v-if="!isEditing">
        Add
      </button>
      <button class="btn bg-yellow-500 text-white font-bold py-3 px-9 rounded-lg"
      @click="editTodo" v-if="isEditing">
        Edit
      </button>
    </div>
    
    <ul v-if="todoArray.length > 0" class="flex items-start justify-start flex-col gap-10">
      <li 
      class="text-2xl font-semibold text-sky-700 flex items-center justify-between w-full"
      v-for="(item, index) in todoArray" :key="item"
      >
      <span>
        {{ index + 1 }}. {{ item }}
      </span>
      <div class="flex items-center justify-center gap-7">
        <button class="btn text-red-500" @click="removeTodo(index)" v-if="!isEditing">
          <i class="fas fa-trash-alt"></i>
        </button>
        <button class="btn text-yellow-500" @click="getTodo(index)">
          <i class="far fa-edit"></i>
        </button>
      </div>
    </li>
    </ul>
    <h1 v-else class="text-center text-3xl text-gray-400">There are no tasks!</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoArray: [
        "Make a cup of coffee",
        "Do a home-work"
      ],
      inputValue: '',
      isEditing: false,
      taskIndex: '',
    }
  },
  methods: {
    addTodo() {
      if (this.inputValue === '') {
        return
      }
      this.todoArray.unshift(this.inputValue)
      this.inputValue = ''
    },
    removeTodo(index) {
      this.todoArray.splice(index, 1)
    },
    getTodo(index) {
      this.inputValue = this.todoArray[index]
      this.isEditing = true
      this.taskIndex = index
    },
    editTodo() {
      this.todoArray[this.taskIndex] = this.inputValue
      this.isEditing = false
      this.inputValue = ''
    }
  }
}
</script>
