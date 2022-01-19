<template>
      <ul>
        <transition-group name="list" tag="ul">
          <TodoItem v-for="item in currentArray" :key="item.id" :item="item" @checked="checkCheck(item)"/>
        </transition-group>
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

.list-enter-active, .list-leave-active {
    transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateY(30px);
}

</style>