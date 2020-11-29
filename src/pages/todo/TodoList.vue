<template>
  <div class="todo-list">
    <div v-for="item of data" :key="item.id" class="list-item m-t-10">
      <div class="delete">
        <div class="line"></div>
      </div>
      <div class="desc">{{item.desc}}</div>
    </div>
  </div>
</template>
<script>
import { toRefs } from 'vue'
export default {
  props: {
    data: {
      type: [Array, Object]
    }
  },
  setup (props) {
    const { data } = toRefs(props)
    return {
      data
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../../style/variable';
.todo-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.desc {
}
.list-item {
  height: 15vh;
  width: 95vw;
  background-color: $bg_white;
  border-radius: 15px 15px 0 15px;
  box-shadow: $boxShadow;
  display: flex;
  flex-direction: column;
}
.list-item:hover {
  .delete {
    opacity: 1;
  }
}
.delete {
  width: 20px;
  height: 20px;
  border-radius: $borderCirCle;
  background-color: $bg_error;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translate(-8px, -8px);
  opacity: 0;
  .line {
    width: 15px;
    height: 5px;
    border-radius: $borderRadius;
    background: $bg_white;
  }
}
</style>