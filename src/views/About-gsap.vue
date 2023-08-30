<template>
  <div class="about">
    <Transition
      appear
      @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
    >
      <h1>About</h1>
    </Transition>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
  </div>
</template>

<script>
import { ref } from 'vue' ;
import gsap from 'gsap';

export default {
  setup() {
    const showTitle = ref(true);

    /* use GSAP for transitions */
    const beforeEnter = (el) => {
      console.log('before enter - set initial state');
      el.style.transform = 'translateY(-60px)';
      el.style.opacity = 0;
    }
    // 使用 done 函式，當 gsap onComplete 時觸發 done，告知 vue 動畫結束
    const enter = (el, done) => {
      console.log('starting to enter - make transition');
      gsap.to(el, {
        duration: 3,
        y: 0,
        opacity: 1,
        ease: 'bounce.out',
        onComplete: done, // 若沒有告訴 vue 結束時間，afterEnter 會直接執行
      });
    }
    const afterEnter = (el) => {
      console.log('after enter');
    }

    return {
      beforeEnter, 
      enter, 
      afterEnter, 
    };
  }
}

</script>

<style>
  .about {
    max-width: 600px;
    margin: 20px auto;
  }
</style>