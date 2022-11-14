<script setup>
import {reactive} from 'vue'

const data = reactive({
  feel: "",
  check: false,
  options: [
    "开心",
    "苦恼",
    "emo",
    "激动",
    "愤怒",
    "忧愁",
    "烦乱",
    "感激",
    "幸福"
  ],
  beFeel: "",
  quotations: [
    "不畏浮云遮望眼，只缘身在最高层。 一一宋·王安石·登飞来峰",
    "衣带渐宽终不悔，为伊消得人憔悴。 一一宋·柳永·凤栖梧",
    "长风破浪会有时，直挂云帆济沧海。 一一唐·李白·行路难",
    "海阔凭鱼跃，天高任鸟飞。 一一唐·僧·云览",
    "天行健，君子以自强不息。 一一周易",
    "少年得志，这正是人生的不幸。从内部来说，它会使他恃才自傲并阻碍他的成材；从外部来说，不信纸干什么事都会引起众人的妒忌。——佐藤春夫",
    "我又愿中国青年只是向上走，不必理会这冷笑和暗箭。 ——鲁迅 ",
    "人生的道路都是由心来描绘的。所以，无论自己处于多么严酷的境遇之中，心头都不应为悲观的思想所萦绕。 ——稻盛和夫",
    "忧愁、顾虑和悲观，可以使人得病；积极、愉快和坚强的意志和乐观的情绪，可以战胜疾病，更可以使人强壮和长寿。 ——巴甫洛夫",
    "既然太阳上也有黑点，“人世间的事情”就更不可能没有缺陷。——车尔尼雪夫斯基"
  ],
  emoTimes: 0
})

function submit() {
  if (data.feel === "") {
    alert("什么都没发生")
    return
  }
  if (data.feel.indexOf("伤") > -1 || data.feel.indexOf("难") > -1 || data.feel.indexOf("痛") > -1
      || data.feel.indexOf("烦") > -1 || data.feel.indexOf("累") > -1 || data.feel.indexOf("无聊") > -1) {
    let num = Math.floor(Math.random() * 10);
    data.emoTimes++
    alert(data.quotations[num])
  }
  data.check = true
}

function changeFeel() {

  if (data.beFeel === "") {
    alert("你还没心情选呢")
    return
  }
  data.feel = data.beFeel
  data.check = true
  if (data.feel == '苦恼' || data.feel == 'emo' || data.feel == '愤怒' || data.feel == '忧愁' || data.feel == '烦乱') {
    let num = Math.floor(Math.random() * 10);
    data.emoTimes++
    alert(data.quotations[num])
    if (data.emoTimes > 2) {
      alert("怎么选了那么多次坏心情，找人聊聊吧，比如我")
    }
  } else {
    alert(`恭喜您！你现在非常${data.feel}！`)
    data.emoTimes = 0
  }
  data.beFeel = ""
}

function reset() {
  data.check = false
  data.feel = ""
  data.beFeel = ""
  data.emoTimes = 0
}

</script>

<template>
  <main>
    <div>
      <span>今天开心吗？</span>
      <span v-if="data.check" style="font-weight: bold;font-size: 24px;color: red">{{ data.feel }} </span>
      <div v-else>
        <input v-model="data.feel" autocomplete="off" class="input" type="text"/>
        <button @click="submit" class="btn ml20">确定</button>
      </div>
      <div>
        <span>你想要获得哪种心情？</span>
        <select v-model="data.beFeel">
          <option value="">选择心情</option>
          <option :value="item" v-for="(item, index) in data.options">{{ item }}</option>
        </select>
      </div>
      <div>
        <button @click="changeFeel" class="btn">开始改变</button>
        <button @click="reset" class="btn ml20">重来一次</button>
      </div>

    </div>
  </main>
</template>

<style scoped>
.result {
  height: 20px;
  line-height: 20px;
  margin: 1.5rem auto;
}

.input-box .btn {
  width: 60px;
  height: 30px;
  line-height: 30px;
  border-radius: 3px;
  border: none;
  margin: 0 0 0 20px;
  padding: 0 8px;
  cursor: pointer;
}

.input-box .btn:hover {
  /*background-image: linear-gradient(to top, #cfd9df 0%, #e2ebf0 100%);*/
  /*color: #333333;*/
}

.input-box .input {
  border: none;
  border-radius: 3px;
  outline: none;
  height: 30px;
  line-height: 30px;
  padding: 0 10px;
  background-color: rgba(240, 240, 240, 1);
  -webkit-font-smoothing: antialiased;
}

.input-box .input:hover {
  border: none;
  background-color: rgba(255, 255, 255, 1);
}

.input-box .input:focus {
  border: none;
  background-color: rgba(255, 255, 255, 1);
}

.ml20 {
  margin-left: 20px;
}
</style>