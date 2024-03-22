<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
    <transition name="fade">
      <div id='pop' v-if="showP">You can do it!</div>
    </transition>
    <button @click="showP = !showP">toggle</button>
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
    const showP = ref(false)

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => showToast.value = false, 3000)
    }

    return { showToast, triggerToast, showP }
  }
}
</script>

<style scoped>
  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-to {
    opacity: 1;
  }
  .fade-enter-active {
    transition: all 2s ease;
  }
  .fade-leave-from {
    opacity: 1;
  }
  .fade-leave-to {
    opacity: 0;
  }
  .fade-leave-active {
    transition: all 2s ease;
  }
  #pop{
    margin-bottom: 5px;
    color: #00A7E1
  }
  .toast-enter-active {
    animation: wobble 0.6s ease
  }

 .toast-leave-from {
    opacity: 1;
    transform: translateY(0);
  } 
  .toast-leave-to {
    opacity: 0;
    transform: translateY(-60px);
  }
  .toast-leave-active {
    transition: all 0.3s ease;
  }

  @keyframes wobble {
    0% {  transform: translateY(-60px); opacity:0}
    50% {  transform: translateY(0px); opacity:1}
    60% {  transform: translateX(10px); }
    70% {  transform: translateX(-10px); }
    80% {  transform: translateX(8px); }
    90% {  transform: translateX(-8px); }
    100% {  transform: translateX(0)}
  }
button{
  border-radius: 15px;
  color:white;
  background-color: #FF9B42;
 border: none;
}
</style>