<template>
  <div class="shopCart">
    <div class="left"></div>
    <div class="ballsWrapper">
      <div v-for="(ball,index) in balls"
           :key="index"
           class="ball-item">
        <transition v-on:before-enter="beforeEnter"
                    v-on:enter="enter"
                    v-on:after-enter="afterEnter">
          <div class="ball"
               v-show="ball.show">
            <div class="inner"></div>
          </div>
        </transition>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'ShopCart',
  data () {
    return {
      balls: [
        { show: false },
        { show: false },
        { show: false },
        { show: false },
        { show: false }
      ],
      dropBalls: []
    }
  },
  methods: {
    dropBall (el) {
      let len = this.balls.length;
      for (let i = 0; i < len; i++) {
        let ball = this.balls[i];
        if (!ball.show) {
          ball.show = true;
          ball.el = el;
          this.dropBalls.push(ball);
          return
        }
      }
    },
    beforeEnter (el) {
      let count = this.balls.length;
      while (count--) {
        let ball = this.balls[count]
        if (ball.show) {
          let rect = ball.el.getBoundingClientRect();
          let x = rect.left - 20;
          let y = -(window.innerHeight - rect.top - 20);
          el.style.display = ""
          el.style.transform = `translate3d(0,${y}px,0)`
          let inner = el.querySelectorAll(".inner")[0]
          inner.style.transform = `translate3d(${x}px,0,0)`
        }
      }
    },
    enter (el) {
      // 触发浏览器重绘
      / * eslint - disable - line * /
      let rf = el.offsetHeight;
      console.log("enter", rf)
      this.$nextTick(() => {
        el.style.transform = 'translate3d(0,0,0)'
        let inner = el.querySelectorAll(".inner")[0]
        inner.style.transform = `translate3d(0,0,0)`
      })
    },
    afterEnter (el) {
      let ball = this.dropBalls.shift()
      if (ball) {
        ball.show = false;
        el.style.display = 'none'
      }
    }

  }
}
</script>

<style scoped lang="scss">
.shopCart {
  width: 100%;
  background-color: rgb(34, 30, 31);
  height: 50px;
  .left {
    width: 50px;
    height: 50px;
    background-color: yellowgreen;
  }
  .ballsWrapper {
    .ball-item {
      .ball {
        position: fixed;
        left: 20px;
        bottom: 20px;
        z-index: 200;
        transition: all 0.4s cubic-bezier(0.49, -0.29, 0.75, 0.41);
        .inner {
          transition: all 0.4s linear;
          width: 20px;
          height: 20px;
          border-radius: 50%;
          background-color: green;
        }
      }
    }
  }
}
</style>
