<template>
  <div style="margin-top: 30px">
    <ul>
      <TodoItem
        v-for="(item, i) of todos"
        v-bind:key="item.id"
        v-bind:item="item"
        v-bind:index="i"
        v-on:remove-item="removeItem"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  props: ["todos"],
  components: { TodoItem },
  methods: {
    removeItem(id) {
      this.$emit("remove-item", id);
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>