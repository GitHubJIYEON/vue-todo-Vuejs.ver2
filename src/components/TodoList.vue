<template>
  <div>
    <TransitionGroup
      name="list"
      tag="ul">
      <li
        v-for="(todoItem, index) in propsdata"
        v-bind:key="todoItem.item"
        class="shadow">
        <i
          class="fa-solid fa-check checkBtn"
          v-on:click="toggleComplete(todoItem, index)"
          v-bind:class="{ checkBtnCompleted: todoItem.completed }"></i>
        <span v-bind:class="{ textCompleted: todoItem.completed }">{{ todoItem.item }}</span>
        <span
          class="removeBtn"
          v-on:click="removeTodo(todoItem, index)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeItem', todoItem, index);
    },
    toggleComplete(todoItem, index) {
      this.$emit('toggleItem', todoItem, index);
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.5s;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
