<template>
  <div class="carControl">
    <transition name="minus">
      <span class="item"
            v-show="count"
            @click="decrease">-</span>
    </transition>
    <transition name="count">
      <span class="item count"
            v-show="count">{{count}}</span>
    </transition>
    <span class="item"
          @click="increase">+</span>
  </div>
</template>

<script>
export default {
  name: 'CarControl',
  props: {
    count: {
      type: Number,
      default: 0
    }
  },
  methods: {
    increase () {
      let val = this.count + 1;
      this.$emit("update:count", val)
      this.$emit("drop", event.target);
    },
    decrease () {
      let val = this.count - 1;
      if (val < 0) val = 0;
      this.$emit("update:count", val)
    }
  }
}
</script>
<style scoped lang="scss">
.minus-enter-active,
.minus-leave-active {
  transition: all 0.5s;
}
.minus-enter,
.minus-leave-to {
  opacity: 0;
  transform: translateX(40px) rotate(360deg);
}
.count-enter-active,
.count-leave-active {
  transition: all 0.5s;
}
.count-enter,
.count-leave-to {
  opacity: 0;
  transform: translateX(10px);
}
.carControl {
  .item {
    display: inline-block;
    width: 20px;
    height: 20px;
    line-height: 20px;
    text-align: center;
    border-radius: 50%;
    background-color: green;
    color: white;
    margin-right: 10px;
    &.count {
      background-color: transparent;
    }
  }
}
</style>
