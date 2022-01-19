<template>
      <ul>
          <TodoItem v-for="item in currentArray" :key="item.id" :item="item" @checked="checkCheck(item)"/>
      </ul>
</template>

<script>
import TodoItem from "./TodoItem.vue"

export default {
    name: 'TodoList',
    components: {TodoItem},
    props: 
            {
            showDone: Boolean,
            currentArray: Array
            },
    methods: {
        checkCheck(item){
            this.$emit('checked', item)
        }
    }
}


</script>

<style scoped>

ul {
    padding: 0;
    width: 100%;
}

</style>