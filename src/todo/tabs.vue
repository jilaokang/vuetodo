<template>
  <div>
    <span id="left">
      <!-- 获取计算属性中的值unFinshTodo -->
        {{unFinshTodo}} item left
    </span>

    <span id="tabss">
        <!-- @click调用本地事件，传入被点击tabs
            :class可变class，传入数组tabs，采用三目运算符进行运算
            :key确认渲染顺序
         -->
        <span
        style="margin:0 10px"
        v-for="tabs of state" 
        :key="tabs"
        :class="[tabs,(filter === tabs) ? 'actived':'']"
        @click="toggleFilter(tabs)"
        >
            {{ tabs }}
        </span>
    </span>

    <!-- 点击调用本地clearAllCompleted事件 -->
    <span id="right" @click="clearAllCompleted()">
        CLear all completed
    </span>
  </div>
</template>

<script>
export default {
  /* 接收外部传入参数：验证type和required */
  props: {
    filter: {
      type: String,
      required: true
    },
    todo: {
      type: Object,
      required: true
    }
  },
  /* 数据存放 */
  data() {
    return {
      state: ["all", "active", "completed"]
    };
  },
  /* 计算属性，返回计算值 */
  computed: {
    unFinshTodo() {
      return this.todo.filter(todo => !todo.completed).length;
    }
  },
  /* 函数集合体 */
  methods: {
    toggleFilter(state) {
      /* 调用父组件传入toogle，传入state */
      this.$emit("toggle", state);
    },

    clearAllCompleted() {
      /* 调用父组件传入的clearAll */
      this.$emit("clearAll");
    }
  }
};
</script>

<style>
.actived {
  color: white;
  background: purple;
  padding: 3px 5px;
  border-radius: 3px;
}

#left,
#right,
#tabss {
  margin: 15px 20px;
}
</style>


