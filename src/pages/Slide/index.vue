<template>
  <div class="slide">
    <transition name="bounce">
      <div :class="['slide-content', isShow ? 'is-show' : 'is-hide']">
        <div v-show="title" class="title">{{title}}</div>
        <slot></slot>
      </div>
    </transition>
    <transition name="fade">
      <div v-show="isShow" @click="hide" class="mask"></div>
    </transition>
  </div>
</template>
<script>
import { toRefs, ref, watch } from 'vue'
export default {
  name: 'Slide',
  props: {
    title: {
      type: String,
      default: 'TODO'
    },
    isShow: {
      type: Boolean,
      default: false
    }
  },
  setup (props, context) {
    const { title, isShow } = toRefs(props)
    watch(isShow, (res) => {
      console.log('isShow', res)
    })
    const hide = () => {
      context.emit('update:isShow')
    }
    return {
      title,
      isShow,
      hide
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../../style/variable';
.slide {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 0;
  z-index: 20;
  display: flex;
  flex-direction: column;
  justify-content: center;
  z-index: 1001;
}
.slide-content {
  border-radius: $borderRadius_15;
  background-color: #fff;
  overflow: hidden;
  box-shadow: $boxShadow;
}
.is-show {
  width: 65vw;
  height: 90vh;
  animation: show 0.5s ease-out;
}
.is-hide {
  animation: hide 0.5s ease-in;
}
@keyframes show {
  from {
    height: 0;
    width: 0;
  }
  to {
    width: 65vw； height：90vh;
  }
}

@keyframes hide {
  from {
    width: 65vw； height：90vh;
  }
  to {
    width: 0;
    height: 0;
  }
}
.title {
  padding: 20px;
}
.mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: $maskColor;
  z-index: -10;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>