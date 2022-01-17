<template>
  <li>
    <input type="checkbox" @click="$emit('checked')" v-model="item.done">
    <h1>{{item.content}}</h1>
  </li>
</template>

<script>
export default {
  data(){return{
    isChecked: false
  }},
  props: {item: Object},
  methods: {}
}
</script>

<style scoped>
  li{
    display:flex;
    padding: 0;
    margin: 0;
  }
  input {
    accent-color: rebeccapurple;
  }
</style>