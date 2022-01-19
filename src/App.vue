<template>
  <div id="app">
  <TodoMenu v-if="menuOpen" @signal="doneToggle" @delete="deleteTodos" @clear="clearTodos" :showDone="showDone" @close="menuOpen = false"/>
    <img class="hamburger" src="./assets/menu.svg" width="20px" alt="Open Menu" @click="menuOpen = true">
    <h2>TEFLON</h2>
    <span>När det inte fastnar</span>
    <p>Du har <b>{{itemsLeft}}</b> todos kvar att göra</p>
    <TodoList :currentArray="currentArray" @checked="checkValue"/>
    <form v-on:submit.prevent="addItem">
      <input type="text" v-model="newItem">
      <button>Add Item</button>
    </form>
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
    newItem: "",
    menuOpen: false
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
  justify-content: center;
  background: gainsboro;
  margin: 0;
}

form {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
  border: solid 1px black;
}

form button {
  font-size: 2rem;
  width: 100%;
  border-style: none;
}

input {
  box-sizing: border-box;
  border-radius: 0;
  border: none;
  width: 100%;
  font-size: 2rem;
}

#app {
  height: 100vh;
  width: 100%;
  position: relative;
  background: tomato;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;  
}

.hamburger {
  align-self: flex-end;
}

</style>