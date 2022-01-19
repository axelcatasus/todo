<template>
  <div class="menu">
    <button @click="$emit('signal')">{{toggle}} done todos</button>
    <button @click="$emit('delete')">Delete done todos</button>
    <button @click="$emit('clear')">Clear all data</button>
  </div>
</template>

<script>
export default {
  data(){return{
    }},
    props:{showDone : Boolean},
      
    computed: {
      toggle(){
        if(!this.showDone){
          return "Show"
        }
          return "Hide"
      }
    }
}
    

</script>

<style scoped>

.menu {
  min-height: 20vh;
  background: tomato;
  padding: 3rem;
  border-radius: 10px;
  border: solid 10px black;
  display: flex;
  flex-direction: column;
  align-items: center;
}

button:hover {
  background: peru;
}
button {
  font-size: 4rem;
}

</style>
