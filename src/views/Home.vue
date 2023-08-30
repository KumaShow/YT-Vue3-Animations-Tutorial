<template>
  <div class="home">
    <Transition name="toast">
      <Toast v-if="showToast" />
    </Transition>
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script>
import { ref } from 'vue'
import Toast from '../components/Toast'
import Todos from '../components/Todos'

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false)

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => showToast.value = false, 3000)
    }

    return { showToast, triggerToast }
  }
}
</script>

<style>
/* 使用 vue transition class */
/* enter */
/* .toast-enter-from {
  opacity: 0;
  transform: translateY(-60px);
}
.toast-enter-to {
  opacity: 1;
  transform: translateY(0px);
}*/
.toast-enter-active {
  /* transition: all 0.3s ease; */
  animation: wobble 0.5s ease;
} 

/* leave */
.toast-leave-from {
  opacity: 1;
  transform: translateY(0px);
}
.toast-leave-to {
  opacity: 0;
  transform: translateY(-60px);
}
.toast-leave-active {
  transition: all 0.3s ease;
} 

/* use key frame */
@keyframes wobble {
  0% { opacity: 0; transform: translateY(-60px);}
  50% { opacity: 1; transform: translateY(0px);}
  60% { transform: translateX(8px); }
  70% { transform: translateX(-8px); }
  80% { transform: translateX(4px); }
  90% { transform: translateX(-4px); }
  100% { transform: translateX(0px); }
}
</style>