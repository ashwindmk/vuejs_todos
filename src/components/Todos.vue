<template>
    <div class="todos">
        <h3> TODOS </h3>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
        </div>
    </div>
</template>

<script>
    import TodoItem from './TodoItem.vue'

    export default {
        name: 'Todos',
        components: {
            TodoItem
        },
        props: ["todos"]
    }
</script>

<style scoped>
    .todos {
        text-align: left;
        margin-left: 80px;
        margin-right: 80px;
    }
</style>
