<template>
  <li>
    <input type="checkbox" @click="$emit('checked')" v-model="item.done">
    {{item.content}}
  </li>
</template>

<script>
export default {
  data(){return{
  }},
  props: {item: Object},
  methods: {}
}
</script>

<style scoped>
  li{
    display: flex;
    align-items: center;
    padding: 1rem;
    margin: 0rem;
    margin-top: .5rem;
    background: lightcoral;
  }
  input {
    accent-color: rebeccapurple;
    width: 40px;
    height: 40px;
  }
  
  .hidden {
    display: none;
  }

  .show {
    display: block;
  }
</style>