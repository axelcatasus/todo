<template>
  <div class="menu">
    <img class="hamburger" src="../assets/close.svg" width="30px" alt="Open Menu" @click="$emit('close')">
    <button @click="$emit('signal')" :class="{hide : showDone, 'show':!showDone}">{{toggle}} done todos</button>
    <button class="delete" @click="$emit('delete')">Delete done todos</button>
    <button class="clear" @click="$emit('clear')">Clear all data</button>
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
  width: 80vw;
  position: absolute;
  background: cornflowerblue;
  top: 0;
  right: 0;
  /* border-radius: 10px; */
  /* border: solid 10px black; */
  display: flex;
  flex-direction: column;
  align-items: center;
  }

.menu-mask{
  
  width: 100%;
  height: 100vh;
  background: rgba(0, 0, 0, .5);
}

img {
  margin: 1rem;
}

button {
  border: none;
  font-size: 1rem;
  text-align: left;
  padding-left: 4rem;
  margin-bottom: 1rem;
  height: 4rem;
  width: 100%;
}

button:hover {
  background-color: lightgray;
}

.hide {
  background: url(../assets/visibility_off.svg) no-repeat center left 2rem rgb(241, 236, 236)	
}

.show {
  background: url(../assets/visibility.svg) no-repeat center left 2rem rgb(241, 236, 236)
}

.delete {
  background: url(../assets/delete.svg) no-repeat center left 2rem rgb(241, 236, 236)
}

.clear {
  background: url(../assets/delete_forever.svg) no-repeat center left 2rem rgb(255, 206, 208);
  margin-top: 20rem;
  
}

</style>
