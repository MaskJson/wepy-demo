<template>
  <view>
    <button @tap="plus">plus</button>
    <button @tap="invoke">直接调用同处一个父组件中的兄弟组件的方法</button>
    <view style="text-align: center"><text>{{num}}</text></view>
  </view>
  <ppp />
</template>

<script>
  import wepy from 'wepy'
  import ppp from './ppp'

  export default class Comp extends wepy.component {
    components = {
      ppp
    };
    props= {
      num: {
        type: Number,
        twoWay: true
      }
    };
    methods = {
      plus() {
        this.$emit('plus');
      },
      invoke() {
        this.$invoke('../ppppp', 'change');
      }
    };
    events = {
      jian() {
        this.num--;
      }
    }
  }
</script>

<style>

</style>
