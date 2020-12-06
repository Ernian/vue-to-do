<template>
  <li>
    <span v-bind:class="{ done: item.completed }">
      <input type="checkbox" v-on:change="item.completed = !item.completed" />
      <strong>{{ index + 1 }}</strong>
      {{ item.title | uppercase }}
    </span>
    <button class="rm" v-on:click="$emit('remove-item', item.id)">
      &times;
    </button>
  </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      require: true,
    },
    index: Number,
  },
  filters: {
    uppercase(string) {
      return string.toUpperCase();
    },
  },
};
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 2rem;
  margin-bottom: 1rem;
}

.rm {
  background: red;
  color: #fff;
  border-radius: 50%;
  font-weight: bold;
}

input {
  margin-right: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>