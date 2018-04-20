<template>
    <div id="root">
        <Header :name="todos.name"/> 

        <Content :todo="filterTodo" @del="delTodo " />

        <Item :todo="todos.todo"/>
        <hr>

        <tabs :todo="todos.todo" :filter="filter" @toggle="toggleFilter" @clearAll="clearAllCompleted" />
    </div>
</template>


<script>
import Header from "./header.vue";
import Content from "./content.vue";
import Item from "./item.vue";
import Tabs from "./tabs.vue";

export default {
  components: {
    Header,
    Content,
    Item,
    Tabs
  },
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

  data() {
    return {
      todos: {
        todo: [],
        name: "钱博康"
      },
      filter: "all"
    };
  },

  methods: {
    delTodo(id) {
      this.todos.todo.splice(
        this.todos.todo.findIndex(todo => todo.id === id),
        1
      );
      console.log(todo);
    },
    toggleFilter(state) {
      this.filter = state;
    },

    clearAllCompleted() {
      this.todos.todo=this.todos.todo.filter(todo => todo.completed === false)
    }
  }
};
</script>

<style>
#root{
  margin: 30px auto;
  text-align: center;
  width: 80%;
}
</style>


