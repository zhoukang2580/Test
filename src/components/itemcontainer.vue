<template>
  <section>
    <header class="top_tips">
      <span class="num_tip" v-if="fatherComponent == 'home'">{{ level }}</span>
      <span class="num_tip" v-if="fatherComponent == 'item'"
        >题目{{ itemNum }}</span
      >
    </header>
    <div v-if="fatherComponent == 'home'">
      <div class="home_logo item_container_style"></div>
      <router-link to="item" class="start button_style"></router-link>
    </div>
    <div v-if="fatherComponent == 'item'">
      <div class="item_bacl item_container_style">
        <div
          class="item_list_container"
          v-if="itemDetail && itemDetail.length > 0"
        >
          <header class="item_title">
            {{ itemDetail[itemNum - 1].topic_name }}
          </header>
          <ul>
            <li
              v-for="(item, index) in itemDetail[itemNum - 1].topic_answer"
              :key="item.topic_answer_id"
              @click="choosed(index, item.topic_answer_id)"
              class="item_list"
            >
              <!-- <span class="option_style" v-bind:class="{ has_choosed: choosed == index }" >{{ choosedType(index) }}</span > -->
              <span
                class="option_style"
                v-bind:class="{ has_choosed: choosedNum == index }"
                >{{ chooseType(index) }}</span
              >
              <span class="option_detail">{{ item.answer_name }}</span>
            </li>
          </ul>
        </div>
      </div>
      <span
        class="next_item button_style"
        @click="nextItem"
        v-if="itemNum < itemDetail.length"
      ></span>
      <span
        class="submit_item button_style"
        v-else
        @click="submitAnswer"
      ></span>
    </div>
  </section>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "itemcontainer",
  data() {
    return {
      itemId: null, //题目ID
      choosedNum: null, //选中答案的索引
      choosedId: null, //选中答案的ID
    };
  },
  props: ["fatherComponent"],
  computed: mapState([
    "itemNum", //第几题
    "level", //第几周
    "itemDetail", //题目详情
    "timer", //计时器
  ]),
  methods: {
    ...mapActions(["addNum", "initializeData"]),
    nextItem() {
      if (this.choosedNum !== null) {
        console.log(this.choosedNum, "===");
        this.choosedNum = null;
        this.addNum(this.choosedId);
      } else {
        alert("你还没选择答案哟");
      }
    },
    chooseType: function (type) {
      switch (type) {
        case 0:
          return "A";
        case 1:
          return "B";
        case 2:
          return "C";
        case 3:
          return "D";
      }
    },
    choosed(type, id) {
      this.choosedNum = type;
      this.choosedId = id;
    },
    submitAnswer() {
      if (this.choosedNum !== null) {
        this.addNum(this.choosedId);
        setInterval(this.timer);
        this.$router.push("score");
      } else {
        alert("你还没选择答案哦");
      }
    },
  },
  created() {
    if (this.fatherComponent == "home") {
      this.initializeData();
      // document.body.style.backgroundImage = 'url(./static/img/1-1.jpg)';只有一个人说了真话。A说B是对的，B说D是对的，C说我是错的，D说B在撒谎。谁说了真话？？
    }
  },
};
</script>

<style lang="less">
.top_tips {
  position: absolute;
  height: 9.35rem;
  width: 5.25rem;
  top: -1.3rem;
  right: 1.6rem;
  background: url(../assets/WechatIMG2.png) no-repeat;
  background-size: 100% 100%;
  z-index: 10;
  .num_tip {
    position: absolute;
    left: 1.38rem;
    bottom: 1.5rem;
    height: 0.7rem;
    width: 2.5rem;
    font-size: 0.8rem;
    font-family: "\9ED1\4F53";
    font-weight: 600;
    color: #a57c50;
    text-align: center;
  }
}

.item_container_style {
  height: 13.625rem;
  width: 21.15rem;
  background-repeat: no-repeat;
  position: absolute;
  top: 8rem;
  left: -0.5rem;
}
.home_logo {
  background-image: url(../assets/1-2.png);
  background-size: 17.5rem 100%;
  background-position: right center;
}

.button_style {
  display: block;
  height: 3.1rem;
  width: 6.35rem;
  background-size: 100% 100%;
  position: absolute;
  top: 20.5rem;
  left: 50%;
  margin-left: -2.4rem;
  background-repeat: no-repeat;
}
.item_bacl {
  background-image: url(../assets/2-1.png);
  background-size: 100% 100%;
}
.start {
  background-image: url(../assets/1-4.png);
}

.next_item {
  background-image: url(../assets/2-2.png);
}
.submit_item {
  background-image: url(../assets/3-1.png);
}
.item_list_container {
  position: absolute;
  height: 7rem;
  width: 8rem;
  top: 2.4rem;
  left: 3rem;
  -webkit-font-smoothing: antialiased;
}
.item_title {
  font-size: 0.65rem;
  color: #00e;
  line-height: 0.7rem;
}
.item_list {
  font-size: 0;
  margin-top: 0.4rem;
  width: 10rem;
  span {
    display: inline-block;
    font-size: 0.6rem;
    color: #00e;
    vertical-align: middle;
  }
  .option_style {
    height: 0.725rem;
    width: 0.725rem;
    border: 1px solid #fff;
    border-radius: 50%;
    line-height: 0.725rem;
    text-align: center;
    margin-right: 0.3rem;
    font-size: 0.5rem;
    font-family: "Arial";
  }
  .has_choosed {
    background-color: #ffd400;
    color: #575757;
    border-color: #ffd400;
  }
  .option_detail {
    width: 7.5rem;
    padding-top: 0.11rem;
  }
}
</style>