<template>
  <div id="app">
    <p>{{itemsLeft}} todos left</p>
    <TodoList :todoItems="todoItems" @checked="checkValue"/>
    <input type="text" v-model="newItem">
    <button @click="addItem">Add Item</button>
    <p>{{newItem}}</p>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {TodoList},
  data(){return{
    todoItems: [],  
    showDone: true,
    newItem: ""
  }},
  beforeMount(){
    if (localStorage.getItem("todos"))
        this.todoItems = JSON.parse(localStorage.getItem("todos"));
  },
  methods: {
    addItem(){
      if(this.newItem===""){
        return
      } else {
      this.todoItems.push({id: this.uuid(), content: this.newItem, done: false})
      }
      this.persist()
    },
    uuid () {
      return Math.random().toString(16).slice(2)
    },
    persist(){
      localStorage.setItem('todos', JSON.stringify(this.todoItems))
    },
    checkValue(korv){
      if(korv.done == true){
        korv.done = false
        this.persist()
      } else {
        korv.done = true
        this.persist()
      }
    }
  },
  computed: {
    itemsLeft(){
      return this.todoItems.filter(items => items.done === false).length
    }
  }
}
</script>

<style>

</style>