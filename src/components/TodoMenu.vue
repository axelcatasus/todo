<template>
  <div class="menu">
    <img class="hamburger" src="../assets/close.svg" width="20px" alt="Open Menu" @click="$emit('close')">
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
  box-sizing: border-box;
  height: 100%;
  width: 80%;
  position: absolute;
  background: DARKsalmon;
  padding: 3rem;
  top: 0;
  right: 0;
  /* border-radius: 10px; */
  /* border: solid 10px black; */
  display: flex;
  flex-direction: column;
  align-items: center;
}

button:hover {
  background: peru;
}
button {
  font-size: 2rem;
  width: 100%;
}

</style>
