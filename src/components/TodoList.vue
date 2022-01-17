<template>
  <div>
      <ul>
          <TodoItem v-for="item in todoItems" :key="item.id" :item="item" @checked="checkCheck(item)"/>
      </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue"
export default {
    name: 'TodoList',
    components: {TodoItem},
    props: ['todoItems'],
    methods: {
        checkCheck(item){
            this.$emit('checked', item)
        }
    }
}


</script>

<style scoped>
ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

</style>