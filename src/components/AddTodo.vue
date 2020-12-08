<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Add Todo...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>


<script>
//not needed anymore, jsonplaceholder API fills todos with data and unique ids
//import { uuid } from 'vue-uuid';
export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            // prevent the form submit to file, i need my own func: make newTodo first, then submit the add-todo event and then call a function in App.vue
            e.preventDefault(); 
            
            const newTodo = {
                //id: uuid.v4(), //not needed anymore, jsonplaceholder API fills todos with data and unique ids
                title: this.title,
                completed: false
            };

            //send up to parent
            this.$emit('add-todo', newTodo);

            // clear text i input into textbox
            this.title = "";

        }

    }
}
</script>


<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2;
    }
</style>