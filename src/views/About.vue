<template>
  <div class="about">
    <transition appear name="fade"
    @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
      @leave="leave"
      @after-leave="afterLeave">
    <h1 v-if="showTitle">About</h1>
    </transition>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
  </div>
</template>

<script>
import { ref } from 'vue'
import gsap from 'gsap'
export default {
  setup() {
    const showTitle = ref(true)

    const beforeEnter = (el) => {
      el.style.opacity = 0
      el.style.transform = 'translateY(-60px)'
    }
    const enter = (el, done) => {
      gsap.to(el, {
        duration: 1,
      y:0,
      opacity:1,
      ease:'bounce.out',
      onComplete: done
      }
      )
    }
    const afterEnter = (el) => {
      el.style.color = 'blue'
      console.log('after enter', el)

      setTimeout(() => showTitle.value = false, 2000)
    }
    const beforeLeave = (el) => {
      el.style.color = "orange"
      console.log('before leave', el)
    }
    const leave = (el) => {
      console.log('leave', el)
    }
    const afterLeave = (el) => {
      console.log('after leave', el)
    }

    return { beforeEnter, enter, afterEnter, beforeLeave, leave, afterLeave, showTitle }
  }
}
</script>


<style>
 .about {
    max-width: 600px;
    margin: 20px auto;
  }

  .fade-enter-from {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 3s ease;
  }
  .fade-leave-to {
    opacity: 0;
  }
  .fade-leave-active {
    transition: opacity 3s ease;
  }
</style>