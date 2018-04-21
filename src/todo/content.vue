<template>
    <div>
        <!-- 循环体 -->
        <div
        v-for="todo in todo"
        :key="todo"
        >
            <!-- v-model双向绑定传入一个数据 -->
            <input type="checkbox" name="" id="" v-model="todo.completed">
            <!-- :class动态传入class -->
            <span :class="[todo.completed?'conpletedList':'']" > {{todo.content}}</span>
            <!-- 执行本地deltodo函数 -->
            <button @click="deltodo"></button>
            
        </div>
    </div>
</template>

<script>
export default {
    /* 接收父组件中的todo */
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods:{
      deltodo(){
          /* 调用父组件中的del函数 */
          this.$emit('del',this.todo.id )
      }
  }
};
</script>


<style>

.conpletedList{
    color: green;
}
</style>
