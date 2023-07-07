<template>
    <div class="hello">
        <div class="add_wrapper">
            <input v-model="newTodo" type="text" class="add_input" placeholder="Write here a new task...">
            <button @click="addTodo" class="btn">Add+</button>
        </div>
        <ul class="todo_list">
            <li class="todo_item" v-for="(todo, index) in todoItems" :key="index">
                <div class="wrapper">
                    <input v-model="todo.isdone" class="checkbox" type="checkbox">
                    <p class="todo_title">{{ todo.title }}</p>
                </div>
                <button @click="deleteTodo(index)" class="btn">Delete</button>
            </li>
        </ul>
    </div>
</template>
  
<script>
export default {
    name: 'ToDo',
    data() {
        return {
            todoItems: [{ title: 'Go to the shop', isdone: false }],
            newTodo: ''
        }
    },
    updated() {
        localStorage.setItem('todos', JSON.stringify(this.todoItems))
    },
    mounted() {
        this.todoItems = JSON.parse(localStorage.getItem('todos'))
        console.log(this.todoItems);
    },
    methods: {
        addTodo() {
            const todoObj = {
                title: this.newTodo,
                isdone: false
            }
            let todoItems = []
            this.newTodo.trim() !== '' ? this.todoItems = this.todoItems || [] ? todoItems += todoObj : this.todoItems.push(todoObj) : document.querySelector('.add_input').classList.add('error');
            input.classList.contains('error') ? setTimeout(() => { input.classList.remove('error') }, 500) : void 0;
            this.newTodo = '';
        },
        deleteTodo(index) {
            this.todoItems.splice(index, 1)
        }
    }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

.add_wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 15px;
}

.wrapper {
    display: flex;
    justify-content: start;
    align-items: center;
    flex-wrap: nowrap;
    flex-direction: row;
    gap: 10px;
    max-width: 100%;
}

input[type="checkbox"] {
    min-width: 20px;
    height: 20px;
    font-size: 0;
}

.todo_title {
    overflow-wrap: anywhere;
}

.todo_list {
    max-width: 500px;
    margin-inline: auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: start;
}

.todo_item {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    gap: 30px;
    margin: 15px 0;
    padding-inline: 15px;
    border-radius: 15px;
    box-shadow: 0 0 5px #000000a0;
}

.btn {
    padding: 5px 10px;
    border-radius: 5px;
    outline: none;
    border: 2px solid #1e67f7;
    background-color: #1e67f7;
    color: #fff;
    letter-spacing: .05em;
    transition: all .2s ease;
}

.btn:hover {
    /* color: #000; */
    background-color: #1c56cc;
}

.btn:active {
    background-color: #1546a6;
}

.add_input {
    outline: none;
    border: 0;
    border-bottom: 3px solid orange;
    padding: 5px;
    font-size: 16px;
    transition: all .3s ease;
}

.add_input:focus {
    border-color: #000;
}

.add_input:focus::placeholder {
    color: #fff;
}

.error {
    animation: error ease .5s;
}

@keyframes error {
    20% {
        transform: translateX(1px);
        border-color: red;
    }

    40% {
        transform: translateX(-1px);
    }

    60% {
        transform: translateX(1px);
    }

    80% {
        transform: translateX(-1px);
        /* border-color: red; */
    }

    100% {
        transform: translateX(1px);
    }
}</style>
  