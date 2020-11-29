<template>
  <div class="add">
    <transition name="component-fade" mode="out-in">
      <div v-show="isAddCont" class="add-content">
        <div class="add-todo">
          <textarea
            autofocus
            v-model="todoValue"
            placeholder="请输入待办流程"
            rows="8"
            cols="20"
            class="add-textarea"
          />
          <button @click="saveTodo" class="save-todo">
            <img src="../../assets/svg/save.svg" width="20" height="20" class="save-icon" />
          </button>
        </div>
      </div>
    </transition>
    <div @click="showAddCont" class="create-btn">
      <div class="across">
        <div class="vertical"></div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from 'vue'
export default {
  name: 'AddTodo',
  setup (props) {
    const isAddCont = ref(false);
    // 展示添加todo
    const showAddCont = () => {
      isAddCont.value = !isAddCont.value
    }
    // 保存todo
    const todoValue = ref(null)
    const saveTodo = () => {
      todoValue.value = '';
      isAddCont.value = ref(false);
      console.log(isAddCont.value)
    }
    return {
      isAddCont,
      showAddCont,
      todoValue
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../../style/variable';
.add {
  height: 60px;
  width: 60px;
  position: fixed;
  right: 10px;
  bottom: 10px;
}
.add-content {
  position: absolute;
  top: -21vh;
  left: -79vw;
  width: 80vw;
  height: 22vh;
  background-color: #fff;
  box-shadow: $boxShadow;
  border-radius: 15px 15px 0 15px;
  overflow: hidden;
}
.create-btn {
  height: 60px;
  width: 60px;
  border-radius: 50%;
  background-color: rgb(250, 250, 250);
  box-shadow: $boxShadow;
  display: flex;
  justify-content: center;
  align-items: center;
}
.slot {
  padding: 5px;
}

.add-todo {
  display: flex;
  overflow: hidden;
  .add-textarea {
    flex: 1;
    width: 95%;
    font-size: 16px;
    border: none;
    text-indent: 6px;
    outline: none;
    resize: none;
  }
  .save-todo {
    width: 40px;
    height: 40px;
    font-size: 12px;
    position: absolute;
    bottom: 0;
    right: 0;
    font-weight: 600;
    border-radius: $borderRadius_15;
    transform: translate(10px, 10px);
    outline: none;
    border: none;
    text-align: center;
    background-color: $bg_purple;
    color: $colorWhite;
    box-shadow: $boxShadow;
    .save-icon {
      margin-left: -5px;
    }
  }
}

.vertical,
.across {
  width: 30px;
  height: 10px;
  background-color: rgb(226, 225, 225);
  border-radius: 15px;
}
.vertical {
  transform: rotate(90deg);
}

.component-fade-enter-active,
.component-fade-leave-active {
  transition: opacity 0.3s ease;
}

.component-fade-enter-from,
.component-fade-leave-to {
  opacity: 0;
}
</style>