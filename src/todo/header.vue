<template>
  <div>
      <h3>
          {{name}} ，的待办事项
      </h3>
  </div>
</template>

<script>
export default {
  /* 从外部接收name */
  props: {
    name: {
      type: String,
      required: true
    }
  }
};

</script>
