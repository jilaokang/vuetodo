<template>
  <div>
    <!-- autofocus自动聚焦
        @keyup键盘事件传入enter键
     -->
      <input type="text"
        autofocus="autofocus"
        placeholder="请输入即将待办的事项"
        @keyup.enter="addtodo"
      >
  </div>
</template>

<script>
let id = 0;
export default {
  /* 接收传入数据 */
  props: {
    /* 传入todo，确认type和required */
    todo: {
      type: Array,
      required: true
    }
  },

  /* 函数集合 */
  methods: {
    /* 传入e，所有事件 */
    addtodo(e) {
      /* unshift在数组第一行加入以下数据 */
      this.todo.unshift({
        id: id++,
        /* e.target表示该DOM元素，在该处取值 */
        content: e.target.value.trim(),
        completed: false
      });
      e.target.value = ""
    }
  }
};
</script>
