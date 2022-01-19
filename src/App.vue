<template>
  <div id="app">
    <transition name="blur">
      <div v-if="menuOpen" @click="menuOpen = false" class="blur"></div>
    </transition>
    <transition name="slide-fade">
      <TodoMenu v-if="menuOpen" @signal="doneToggle" @delete="deleteTodos" @clear="clearTodos" :showDone="showDone" @close="menuOpen = false"/>
    </transition>
      <img class="hamburger" src="./assets/menu.svg" alt="Open Menu" @click="menuOpen = true">
      <img class="logo" src="./assets/teflon-panna.svg" width="100px">
      <h1 class="header">TEFLON</h1>
      <span>När det inte fastnar</span>
      <p>Du har <b>{{itemsLeft}}</b> todos kvar att göra</p>
      <TodoList :currentArray="currentArray" @checked="checkValue"/>
      <transition name="add-item">
        <form v-on:submit.prevent="addItem">
          <input type="text" v-model="newItem">
          <button>Lägg till todo</button>
        </form>
      </transition>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import TodoMenu from './components/TodoMenu.vue'

export default {
  name: 'App',

  // LÄGG IN TODOMENU HÄR NERE! ALDRIG I LIVET!!!!!!!!!
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
@import url('https://fonts.googleapis.com/css2?family=Titillium+Web&display=swap');

* {
  font-family: 'Titillium Web', sans-serif;
 
}


.blur {
  position: absolute;
  background: rgba(0, 0, 0, .5);
  width: 100%;
  height: 100%;
  transition: all 1000ms;
}

body {
  min-height: 100vh;
  /* display: flex; */
  justify-content: center;
  background: gainsboro;
  margin: 0 auto;
  padding: 0;
}


#app {
  height: 100vh;
  /* width: 100vw; */
  position: relative;
  background: white;
  padding: 0 1rem 0 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 1
}

.header{
  font-size: 3rem;
  margin: 0;
}

span{
  font-size: .8rem;
  margin-bottom:2rem;
}

p{
  font-size: 1rem;
  margin: 0;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  border: solid 1px black;
  margin-top: .5rem;
  align-self: stretch;
}

form button {
  font-size: 1rem;
  color: white;
  height: 3rem;
  width: 100%;
  border-style: none;
  background: rgb(34, 34, 34);
}

form button:hover {
  background: rgb(54, 54, 54);
}

input {
  box-sizing: border-box;
  border-radius: 0;
  border: none;
  width: 100%;
  font-size: 1rem;
  height: 3rem;
  text-align: center;
  outline: none;
}

.hamburger {
  position: fixed;
  top: 0rem;
  right: 1rem;
  align-self: flex-end;
  margin-top: 1rem;
  width: 2.5rem;
}

.hamburger:hover {
  filter:opacity(.5)
}

.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .3s ease;
}

.slide-fade-enter {
  transform: translateX(30rem);
  transition: all .3s ease;
  opacity: 1;
}

.slide-fade-leave-to {
  transform: translateX(30rem);
  transition: all .3s ease;
  opacity: 1;
}

.blur-enter {
  background: none;
}

.blur-enter-active {
  transition: all .3s ease;
}

.blur-leave-active {
  transition: all .3s ease;
}

.blur-leave-to {
  background: none;
}



</style>