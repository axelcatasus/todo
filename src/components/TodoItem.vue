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
    padding: .5rem;
    margin: 0.5rem 0;
    background: gainsboro;
  }
  input {
    accent-color: darkgray;
    width: 20px;
    height: 20px;
  }
  
  .hidden {
    display: none;
  }

  .show {
    display: block;
  }
</style>