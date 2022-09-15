<template>
  <div class="tile" :class="{ checked: todoComponent.checked }">
    <div class="tile-icon">
      <i
        class="icon"
        :class="todoComponent.checked ? 'icon-check' : 'icon-time'"
      ></i>
    </div>
    <div class="tile-content">
      <div class="tile-subtitle">{{ todoComponent.description }}</div>
      <div>{{ todoComponent.checked }}</div>
    </div>
    <div class="tile-action">
      <button @click="$emit('toggle', todoComponent)" class="btn btn-link">
        Concluído
      </button>
      <button @click="$emit('remove', todoComponent)" class="btn btn-link">
        <span class="text-error">Remover</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todoComponent: { type: Object, required: true },
  },
};
</script>

<style scoped>
.checked {
  text-decoration: line-through;
  color: lightgray;
}
</style>
