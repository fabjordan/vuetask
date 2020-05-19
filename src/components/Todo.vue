<template>
  <div class="tile flex-centered p-1 item" :class="{ checked: todo.checked }">
    <div class="tile-icon">
      <span v-if="!todo.checked">
        <i class="icon icon-time"></i>
      </span>
      <span v-else>
        <i class="icon icon-check"></i>
      </span>
    </div>

    <div class="tile-content">
      <div class="tile-subtitle">{{ todo.description }}</div>
    </div>

    <div class="tile-action">
      
      <button type="button" @click="$emit('toggle', todo)" class="btn btn-success mr-1">
        <span v-if="!todo.checked">
          <i class="icon icon-check"></i>
        </span>
        <span v-else>
          <i class="icon icon-refresh"></i>
        </span>
      </button>

      <button type="button" @click="$emit('delete', todo.id)" class="btn btn-error">
        <i class="icon icon-cross"></i>
      </button>

    </div>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.checked {
  text-decoration: line-through;
  color: lightslategray;
}
</style>