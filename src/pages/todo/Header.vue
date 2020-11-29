<template>
  <div class="todo-header">
    <div @click="handleUserClick" class="user-info m-l-10"></div>
    <div class="title">title</div>
    <div class="operator"></div>
  </div>
</template>
<script>
export default {
  name: 'Header',
  setup (props, context) {
    const handleUserClick = () => {
      context.emit('user-click')
    }
    return {
      handleUserClick
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../../style/variable';
.todo-header {
  height: 5vh;
  line-height: 5vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .user-info {
    width: 30px;
    height: 30px;
    background-color: $bg_white;
    box-shadow: $boxShadow;
    border-radius: $borderRadius;
  }
  .title {
    flex: 1;
  }
  .operator {
    width: 30px;
    height: 30px;
  }
}
</style>