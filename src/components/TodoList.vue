<template>
  <div>
    <ul>
      <li>todo 1</li>
      <todo-item />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  components: { TodoItem },
};
</script>