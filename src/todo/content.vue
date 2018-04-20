<template>
    <div>
        <div
        v-for="todo in todo"
        :key="todo"
        >
            <input type="checkbox" name="" id="" v-model="todo.completed">
            <span :class="[todo.completed?'conpletedList':'']" > {{todo.content}}</span>

            <button @click="deltodo"></button>
            
        </div>
    </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods:{
      deltodo(){
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
