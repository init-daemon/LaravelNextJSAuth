<template>
    <v-row align="center">
        <v-col cols="12" md="6">
            <v-card>
                <v-card-title primary-title>
                    To do list
                </v-card-title>
                <v-card-text>
                    <v-text-field v-model="taskToAdd" name="name" label="Saisir une tâche" id="id"
                        @keypress.enter="addTodo"></v-text-field>
                    <v-btn color="success" @click="addTodo">Entrer une tâche</v-btn>
                    <v-list>
                        <v-list-item v-for="(todo, i) in uncheckedTodo" :key="i" :title="todo.text" @click="toggle(todo.i)">
                            {{ todo.text }}
                        </v-list-item>
                    </v-list>
                    <v-divider></v-divider>
                    <v-list>
                        <v-list-item v-for="(todo, i) in chekedTodo" :key="i" :title="todo.text" @click="toggle(todo.i)">
                            {{ todo.text }}
                        </v-list-item>
                    </v-list>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
import { mapMutations } from 'vuex'

export default {
    data() {
        return {
            checkedTask: [],
            taskToAdd: ''
        }
    },
    computed: {
        todos() {
            return this.$store.state.todos.list
        },
        uncheckedTodo() {
            return this.todos
                .map((task, i) => { return { ...task, i } })
                .filter(task => !task.done)
        },
        chekedTodo() {
            return this.todos
                .map((task, i) => { return { ...task, i } })
                .filter(task => task.done)
        }
    },
    methods: {
        addTodo(e) {
            if (this.taskToAdd)
                this.$store.commit('todos/add', this.taskToAdd)
            this.taskToAdd = ''
        },
        ...mapMutations({
            toggle: 'todos/toggle'
        }),
        checkTask(i) {
            if (this.checkedTask.index(i) == -1)
                this.checkedTask.push(i);
        }
    }
}
</script>
  
<style>
.done {
    text-decoration: line-through;
}
</style>
  