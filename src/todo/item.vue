<template>
  <div>
      <input type="text" name="" id=""
        autofocus="autofocus"
        placeholder="请输入即将待办的事项"
        @keyup.enter="addtodo"
      >
        

  </div>
</template>

<script>
let id = 0;
export default {
  props: {
    todo: {
      type: Array,
      required: true
    }
  },

  methods: {
    addtodo(e) {
      this.todo.unshift({
        id: id++,
        content: e.target.value.trim(),
        completed: false
      });
      e.target.value = ""
    }
  }
};
</script>
