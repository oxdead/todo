<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <!-- <input type="checkbox" v-on:change="markComplete"> -->
            <input type="checkbox" v-on:change="markTodo">
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)" class="del">x</button>
        </p>
    </div>
</template>


<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods: {
        // markComplete() {
        //     // Unexpected mutation of "todo" prop  vue/no-mutating-props
        //     this.todo.completed = !this.todo.completed;
        // },

        // to prevent: Unexpected mutation of "todo" prop  vue/no-mutating-props
        // it's a bad practice to modify a prop, that doesn't belong to component
        // todo: this can be solved too by using 'computed:' property ?
        markTodo() {
            //console.log(this.todo.id);
            //console.log(this.todo.completed);
            this.$emit('mark-todo', this.todo.id);
        }
    }
    
    
}
</script>


<style scoped>
    .todo-item{
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }

    .is-complete{
        text-decoration: line-through;
    }

    .del{
        background: #ff0000;
        color: #ffff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
</style>