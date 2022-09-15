<template>
  <div class="" id="app">
    <div class="container grid-xs py-2">
      <img class="img-responsive img-logo" src="@/assets/logo.png" alt="Logo" />
      <form @submit.prevent="addTodo(todoComponent)">
        <div class="input-group">
          <input
            type="text"
            v-model="todoComponent.description"
            class="form-input"
            placeholder="Novo todo"
          />
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
      </form>
      <div class="todo-list">
        <todoComponent
          v-for="t in todos"
          :key="t.id"
          @toggle="toggleTodo"
          @remove="removeTodo"
          :todoComponent="t"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TodoComponent from "./components/TodoComponent";

export default {
  name: "app",
  components: { TodoComponent },
  data() {
    return { todos: [], todoComponent: { checked: false } };
  },
  methods: {
    addTodo(todoComponent) {
      todoComponent.id = Date.now();
      this.todos.push(todoComponent);
      this.todoComponent = { checked: false };
    },

    toggleTodo(todoComponent) {
      const index = this.todos.findIndex(
        (item) => item.id === todoComponent.id
      );
      if (index > -1) {
        const checked = !this.todos[index].checked;
        this.$set(this.todos, index, { ...this.todos[index], checked });
      }
    },
    removeTodo(todoComponent) {
      const index = this.todos.findIndex(
        (item) => item.id === todoComponent.id
      );
      if (index > -1) {
        this.$delete(this.todos, index);
      }
    },
  },
};
</script>
<style scoped>
.img-logo {
  max-width: 200px;
  margin: 0 auto;
}

.todo-list {
  padding-top: 2rem;
}
</style>
