<template>
    <div id="root">
        <!-- :name="todos.name"传入name给子组件 -->
        <Header :name="todos.name"/> 

        <!-- 传入事件delTod给子组件，子组件调用del执行，用于访问更改父组件数据 -->
        <Content :todo="filterTodo" @del="delTodo " />

        <Item :todo="todos.todo"/>

        <!-- 采用toggle和clearAll调用父组件的toggleFilter和clearAllCompleted两个事件 -->
        <tabs :todo="todos.todo" :filter="filter" @toggle="toggleFilter" @clearAll="clearAllCompleted" />
    </div>
</template>


<script>
/* 引入子组件 */
import Header from "./header.vue";
import Content from "./content.vue";
import Item from "./item.vue";
import Tabs from "./tabs.vue";

export default {
  /* 注册组件 */
  components: {
    Header,
    Content,
    Item,
    Tabs
  },
  /* 计算属性，所得的为值 */
  computed: {
    filterTodo() {
      if (this.filter === "all") {
        return this.todos.todo;
      }
      // 给completed 赋值 (this.filter === "completed") 的结果
      const completed = this.filter === "completed";
      console.log(completed, this.filter, "completed");

      /* 
      * 在todo中过滤数据，传入（todo） => completed === todo.completed 
      * completed为true时候生效
      * todo中符合completed === todo.completed 条件的
      */

      return this.todos.todo.filter(todo => completed === todo.completed);
    }
  },
  /* 父组件数据 */
  data() {
    return {
      todos: {
        todo: [],
        name: "钱博康"
      },
      filter: "all"
    };
  },

  /* 函数集合 */
  methods: {
    /* 删除按钮执行删除该todo */
    delTodo(id) {
      /* splice(起始点，删除个数) */
      this.todos.todo.splice(
        /* findIndex(符合条件) 寻找索引号 */
        this.todos.todo.findIndex(todo => todo.id === id),
        1
      );
      console.log(todo);
    },

    /* 点击切换state及样式 */
    toggleFilter(state) {
      this.filter = state;
    },

    /* 清除所有完成的事件 */
    clearAllCompleted() {
      /* arr.filter(符合条件) 筛选已完成 */
      this.todos.todo = this.todos.todo.filter(
        /* 传入列表，检测todo.completed值 */
        todo => todo.completed === false
      );
    }
  }
};
</script>

<style>
#root {
  margin: 30px auto;
  text-align: center;
  width: 80%;
}
</style>


