<template>
  <div>
    <p>{{message}}</p>
    <div v-if="error">[if block]</div>
    <div :class="error_class">error2</div>
    <p>{{ now }}</p>
    <button @click="time">現在時刻を表示する</button>

    <div style="padding: 30px 0 0">
      <button @click="shuffle">シャッフル</button>
      <transition-group name="flip-list" tag="ul">
        <li v-for="item in items" :key="item.id">{{ item.name }}</li>
      </transition-group>
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      script: [
        {src: "https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.15/lodash.min.js"}
      ]
    }
  },
  data(){
    return {
      message: 'Hello World',
      error: true,
      error_class: 'error',
      now: "00:00:00",
      items: [
        {id: 1, name: "北海道"},
        {id: 2, name: "青森県"},
        {id: 3, name: "岩手県"},
        {id: 4, name: "宮城県"},
        {id: 5, name: "秋田県"},
        {id: 6, name: "山形県"},
        {id: 7, name: "福島県"},
      ]
    }
  },
  methods: {
    time: function(e) {
      let date = new Date();
      this.now = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`
    },
    shuffle: function() {
      this.items = _.shuffle(this.items);
    }
  }
}
</script>

<style>
.error {
  color: red;
}
.flip-list-move {
  transition: transform .5s;
}
</style>
