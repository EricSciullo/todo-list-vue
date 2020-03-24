<template>
  <div id="todo-list" class="container">
    <div class="row">
      <div class="col-md-8 mx-auto">
        <h1 class="text-center display-4">My Todos</h1>
        <form class="input-group" @submit.prevent="addNewTodo">
          <input
            v-model="inputTodo"
            required type="text"
            maxlength="50"
            id="Todonameinput"
            class="col-md-10 form-control"
            placeholder="New Todo"
            aria-describedby="basic-addon"
            autofocus
            ref="todo"
          >

          <button
            v-if="!this.isUpdating"
            @click.prevent="addNewTodo"
            type="button"
            class="input-group-append btn btn-success col-md-2 font-weight-bold"
          >
            Submit
          </button>
          <button
            v-else
            @click.prevent="updateTodoName()"
            type="button"
            class="input-group-append btn btn-primary col-md-2 font-weight-bold"
          >
            Update
          </button>

        </form>

        <table class="table table-sm table-dark">
          <tr v-for="todo in todos" :key="todo.id">
            <td class="form-control-lg">
              <button
                class="btn btn-secondary"
                :class="{ 'btn-success': todo.completed }"
                title="Click to mark as complete"
                @click="editTodoCompletion(todo.id)"
              >
                <span class="fa fa-check"></span>
              </button>
              {{todo.name}}
            </td>

            <td class="text-right">

              <button
                class="btn btn-primary update-todo-btn"
                title="Update Todo"
                @click="editTodoName(todo.id, todo.name)"
              >
                <span class="fa fa-edit"></span>
              </button>

              <button
                class="btn btn-danger"
                title="Delete Todo"
                @click="deleteTodo(todo.id)"
              >
                <span class="fa fa-trash"></span>
              </button>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Todos',
  data() {
    return {
      todos: [],
      id: 0,
      inputTodo: '',
      isUpdating: false,
    };
  },
  mounted() {
    this.getTodos();
  },
  methods: {
    getTodos() {
      this.todos = JSON.parse(sessionStorage.getItem('todos'));
      if (!this.todos) this.todos = [];
    },
    updateTodos() {
      sessionStorage.setItem('todos', JSON.stringify(this.todos));
      this.inputTodo = '';
    },
    addNewTodo() {
      if (this.isUpdating) this.updateTodoName();
      else {
        this.todos.push({ id: this.todos.length, name: this.inputTodo, completed: false });
        this.updateTodos();
      }
    },
    editTodoName(id, name) {
      this.id = id;
      this.inputTodo = name;
      this.isUpdating = true;
      this.$refs.todo.focus();
    },
    updateTodoName() {
      const index = this.todos.findIndex((item) => item.id === this.id);
      this.todos[index].name = this.inputTodo;
      this.updateTodos();
      this.isUpdating = false;
    },
    editTodoCompletion(id) {
      const index = this.todos.findIndex((item) => item.id === id);
      this.todos[index].completed = !this.todos[index].completed;
      this.updateTodos();
    },
    deleteTodo(id) {
      const index = this.todos.findIndex((item) => item.id === id);
      this.todos.splice(index, 1);
      this.updateTodos();
    },
  },
};
</script>

<style scoped>
  .container {
    margin-top: 10vh;
  }

  h1 {
    color: white;
    padding-bottom: 12px;
  }

  .input-group {
    display: flex;
    flex-direction: row;
  }

  button {
    justify-content: center;
  }

  .update-todo-btn {
    margin-right: 4px;
  }

  table {
    border-radius: 4px;
  }
</style>
