<template>
  <div class="todo">
    <Header :data="headerData" @user-click="handleUserClick" class="todo-header" ref="listRef" />
    <div class="list">
      <todo-list :data="todoData"></todo-list>
      <add-todo ref="addRef"></add-todo>
      <slide :isShow="slideIsShow" @update:isShow="setSlideShow"></slide>
    </div>
  </div>
</template>
<script>
import { reactive, defineAsyncComponent, ref, onMounted } from 'vue'
import Header from './todo/Header.vue'
import TodoList from './todo/TodoList.vue'
import AddTodo from './todo/AddTodo.vue';
const Slide = defineAsyncComponent(() => import('./Slide/index.vue'));
export default {
  components: {
    Header,
    TodoList,
    Slide: Slide,
    AddTodo,
    Slide
  },
  setup (props, context) {
    const state = reactive({
      headerData: {
        title: 'title'
      },
      todoData: [
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
        {
          desc: '123',
          id: Math.ceil(Math.random() * 10000)
        },
      ]
    })
    // 操作用户点击设置
    const slideIsShow = ref(false);
    const setSlideShow = (val) => {
      slideIsShow.value = false
    }
    const handleUserClick = () => {
      slideIsShow.value = true;
    }
    // 监听scolltop 固定title栏
    const listRef = ref(null);
    window.addEventListener('scroll', (e) => {
      const el = listRef.value.$el;
      const scrollTop = document.documentElement.scrollTop;
      const maxTop = 40; // 距离顶部的高度
      if (scrollTop < 40) {
        el.style.position = 'static';
      } else {
        el.style.position = 'fixed';
      }
    })

    // 监听添加框失去焦点
    const addRef = ref(null);
    onMounted(() => {
      console.log('addRef', addRef.value)
    })

    return {
      ...state,
      slideIsShow,
      setSlideShow,
      handleUserClick,
      listRef,
      addRef,
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../style/variable';
.todo {
  display: flex;
  flex-direction: column;
  .todo-header {
    width: 100%;
    height: 40px;
    background-color: $bg_white;
    border-radius: 0 0 5px 5px;
    background-color: $bg_purple;
    color: $bg_white;
    font-size: 18px;
    font-weight: 600;
    z-index: 1000;
  }
  .list {
    flex: 1;
    overflow-y: auto;
  }
}
</style>