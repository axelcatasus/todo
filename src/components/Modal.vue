<template>
  <div id="app">
    <div v-if="showModal" class="modalmask" @click="showModal = false"></div>
      <button v-if="!showModal" @click="showModal = true">Modal plz</button>
    <transition name="bounce">
      <div class="modal" v-if="showModal">
        <h1>Nu är den öppen!! Men lådan e stängd</h1>
        <img src="../assets/closed.jpg" alt="" srcset="">
        <p>Lorem, ipsum dolor sit amet consectetur adipisicing elit. Veniam eaque dolorem amet repellendus inventore est labore, voluptatibus corporis officia asperiores repudiandae eum sed suscipit vero earum nostrum quos ipsum voluptatum! </p>
        <button @click="showModal = false">No more modal</button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data(){return{
    showModal: false
  }},
  methods:{

  }

}
</script>

<style scoped>
body,#app{
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background:linear-gradient(cornflowerblue, pink);
}

.modalmask {
  width: 100%;
  height: 100%;
  position: fixed;
  background: rgba(0, 0, 0, .5);
}


.modal {
  position: fixed;
  width: 60%;
  height: 70%;
  background: #EEEEEE;
  padding: 1rem;
}

button{
  padding: 1rem 20rem;
  background-color: tomato;
  border-radius: 50%;
}

.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>