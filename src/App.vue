<template>
  <div class="wrapper">
  <div id="app">
    <h2>TEFLON</h2>
    <span>När det inte fastnar</span>
    <p>{{itemsLeft}} todos left</p>
    <TodoList :currentArray="currentArray" @checked="checkValue"/>
    <form v-on:submit.prevent="addItem">
      <input type="text" v-model="newItem">
      <button>Add Item</button>
    </form>
  </div>
  <TodoMenu @signal="doneToggle" @delete="deleteTodos" @clear="clearTodos" :showDone="showDone"/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import TodoMenu from './components/TodoMenu.vue'

export default {
  name: 'App',

  // LÄGG IN TODOMENU HÄR NERE
  components: {TodoList, TodoMenu},
  data(){return{
    todoItems: [],  
    showDone: true,
    newItem: ""
  }},
  beforeMount(){
    if(localStorage.getItem("showDone")){
      this.showDone = JSON.parse(localStorage.getItem("showDone"))
    }
    if (localStorage.getItem("todos")){
      this.todoItems = JSON.parse(localStorage.getItem("todos"));
    }
  },
  methods: {
    addItem(){
      if(this.newItem===""){
        return
      } else {
      this.todoItems.push({id: this.uuid(), content: this.newItem, done: false})
      }
      this.persist()
      this.newItem = ""
    },
    uuid () {
      return Math.random().toString(16).slice(2)
    },
    persist(){
      localStorage.setItem('todos', JSON.stringify(this.todoItems))
    },
    checkValue(e){
      e.done = !e.done
      this.persist()
    },
    doneToggle(){
      this.showDone = !this.showDone
      localStorage.setItem('showDone', JSON.stringify(this.showDone))

    },
    deleteTodos(){
      this.todoItems = this.todoItems.filter(items => items.done === false)
      this.persist()
    },
    clearTodos() {
      this.todoItems = []
      this.persist()
    }


    },
  computed: {
    itemsLeft(){
      return this.todoItems.filter(items => items.done === false).length
    },
    currentArray(){
      if(!this.showDone){
        return this.todoItems.filter(items => items.done === false)
      } 
      else {
        return this.todoItems
      }
    }
  }
}

</script>

<style>

body {
  min-height: 100vh;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  background: gainsboro;
  font-size: 3rem;
}

#app {
  background: tomato;
  padding: 3rem;
  border-radius: 10px;
  border: solid 10px black;
  display: flex;
  flex-direction: column;
}


</style>