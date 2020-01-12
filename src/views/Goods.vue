<template>
  <div class="home">
    <div class="header"></div>
    <div class="content">
      <div class="menuWrapper"
           ref="menuWrapper">
        <div class="menu">
          <div class="menuItem"
               :class="{active:currentIndex==index}"
               v-for="(item,index) in menuList"
               :key="item.id"
               @click="clickMenu(index)">
            {{item.name}}
          </div>
        </div>
      </div>
      <div class="foodWrapper"
           ref="foodWrapper">
        <div class="food">
          <div class="categaryItem"
               v-for="categaryItem in foodList"
               :key="categaryItem.id">
            <div class="title">{{categaryItem.title}}</div>
            <div class="foodItem"
                 v-for="foodItem in categaryItem.food"
                 :key="foodItem.id">
              <span>{{foodItem.name}}</span>
              <CarControl @drop="drop"
                          :count.sync='foodItem.count'></CarControl>
            </div>
          </div>
        </div>
      </div>
    </div>
    <ShopCart ref="shopCart"></ShopCart>
  </div>
</template>

<script>
import CarControl from "@/components/CarControl.vue"
import ShopCart from "@/components/ShopCart.vue"
import BScroll from "better-scroll";
export default {
  name: 'goods',
  components: {
    CarControl,
    ShopCart
  },
  created () {
    // 此属性不需要作为响应式
    this.foodHeights = []
  },
  data () {
    return {
      menuScroll: "",
      foodScroll: "",
      scrollY: 0,
      currentIndex: 0,
      scrollEnd: false,
      clickLast: false,
      menuScrollFlag: false,
      menuList: [
        { name: "种类1", id: 1 },
        { name: "种类2", id: 2 },
        { name: "种类3", id: 3 },
        { name: "种类4", id: 4 },
        { name: "种类5", id: 5 },
        { name: "种类6", id: 6 },
        { name: "种类7", id: 7 },
        { name: "种类8", id: 8 },
        { name: "种类9", id: 9 },
        { name: "种类10", id: 10 },
        { name: "种类11", id: 11 },
        { name: "种类12", id: 12 },
      ],
      foodList: [
        {          id: 1, title: "种类1", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
          ]        },
        {          id: 2, title: "种类2", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 }
          ]        },
        {          id: 3, title: "种类3", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 }
          ]        },
        {          id: 4, title: "种类4", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 }
          ]        },
        {          id: 5, title: "种类5", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 }
          ]        },
        {          id: 6, title: "种类6", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
          ]        },
        {          id: 7, title: "种类7", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 },
            { name: "food7", id: 7, count: 0 }
          ]        },
        {          id: 8, title: "种类8", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
          ]        },
        {          id: 9, title: "种类9", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 }
          ]        },
        {          id: 10, title: "种类10", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
          ]        },
        {          id: 11, title: "种类11", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 },
            { name: "food7", id: 7, count: 0 },
            { name: "food8", id: 8, count: 0 }
          ]        },
        {          id: 12, title: "种类12", food: [
            { name: "food1", id: 1, count: 0 },
            { name: "food2", id: 2, count: 0 },
            { name: "food3", id: 3, count: 0 },
            { name: "food4", id: 4, count: 0 },
            { name: "food5", id: 5, count: 0 },
            { name: "food6", id: 6, count: 0 }
          ]        },
      ]
    }
  },
  mounted () {
    this.initScroll();
    this.calculateHeights()
  },
  methods: {
    drop (target) {
      this.$refs.shopCart.dropBall(target);
    },
    initScroll () {
      this.menuScroll = new BScroll(this.$refs.menuWrapper, {
        click: true
      })
      this.foodScroll = new BScroll(this.$refs.foodWrapper, {
        probeType: 3,
        click: true
      })
      this.foodScroll.on("scroll", (pos) => {
        this.scrollY = Math.abs(pos.y);
      })
      this.menuScroll.on("scrollStart", () => {
        console.log("菜单开始滚动")
        this.menuScrollFlag = true;
      })
      this.menuScroll.on("scroll", () => {
        console.log("菜单开始滚动")
        this.menuScrollFlag = true;
      })
      this.menuScroll.on("scrollEnd", () => {
        console.log("菜单结束滚动");
        this.menuScrollFlag = false;
      })
      this.foodScroll.on("scrollStart", () => {
        this.scrollEnd = false;
      })
      this.foodScroll.on("scrollEnd", () => {
        console.log("滚动完成")
        this.$nextTick(() => {
          this.clickLast = false;
        })

      })
    },
    calculateHeights () {
      let domArray = document.querySelectorAll(".food .categaryItem");
      let height = 0;
      this.foodHeights.push(height);
      for (let i = 0; i < domArray.length; i++) {
        height += domArray[i].clientHeight;
        this.foodHeights.push(height);
      }
    },
    clickMenu (index) {
      let domArray = document.querySelectorAll(".food .categaryItem");
      let el = domArray[index];
      if (index == domArray.length - 1) {
        console.log("点击最后一个");
        this.clickLast = true;
      } else {
        this.clickLast = false;
      }
      this.foodScroll.scrollToElement(el, 300);
    },
    initMenuScroll (index) {
      let menuArray = document.querySelectorAll(".menu .menuItem");
      let el = menuArray[index];
      this.menuScroll.scrollToElement(el, 300)
    }
  },
  computed: {
  },
  watch: {
    scrollY (val) {
      for (let i = 0; i < this.foodHeights.length; i++) {
        let height1 = this.foodHeights[i];
        let height2 = this.foodHeights[i + 1];
        if (!height2 || (val >= height1 && val < height2)) {
          this.initMenuScroll(i)
          if (this.clickLast) {
            console.log("------", this.foodList.length - 1)
            this.currentIndex = this.foodList.length - 1;
            return
          }
          this.currentIndex = i;
          return
        }
      }
      this.currentIndex = 0;
    },
    foodList () {
      this.calculateHeights()
    }
  }
}
</script>
<style lang="scss">
.home {
  .header {
    width: 100%;
    background-color: rgb(34, 30, 31);
    height: 150px;
  }
  .content {
    display: flex;
    height: calc(100vh - 200px);
    overflow: hidden;
    .menuWrapper {
      width: 100px;
      .menu {
        .menuItem {
          height: 50px;
          line-height: 50px;
          background-color: #ccc;
          text-align: center;
          box-sizing: border-box;
          border-bottom: 1px solid gray;
          &.active {
            background-color: red;
          }
        }
      }
    }
    .foodWrapper {
      flex: 1;
      .food {
        text-align: right;

        .title {
          height: 30px;
          line-height: 30px;
          background-color: green;
        }
        .foodItem {
          height: 60px;
          line-height: 60px;
          background-color: yellowgreen;
          box-sizing: border-box;
          border-bottom: 1px solid gray;
          display: flex;
          justify-content: space-between;
        }
      }
    }
  }
}
</style>
