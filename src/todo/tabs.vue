<template>
<div>

  <span id="left">
       {{unFinshTodo}} item left
  </span>
  <span id="tabss">
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

  <span id="right" @click="clearAllCompleted()">
      CLear all completed
  </span>
</div>
    
</template>

<script>
export default {
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
  data() {
    return {
      state: ["all", "active", "completed"]
    };
  },
  computed: {
    unFinshTodo() {
      return this.todo.filter(todo => !todo.completed).length;
    }
  },
  methods: {
    toggleFilter(state) {
        this.$emit('toggle',state);
    },

    clearAllCompleted() {
        this.$emit('clearAll')
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
#tabss{
    margin: 15px 20px;
}
</style>


