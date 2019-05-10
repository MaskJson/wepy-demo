<style lang="less">
  .container {
    display: flex;
    align-items: center;
  }
  .inline-block {
    display: inline-block;
  }
</style>
<template>
  <view class="container">
    <button class="inline-block" @tap="numHandler({{true}})">+</button>
    <text class="inline-block">{{num}}</text>
    <button class="inline-block" @tap="numHandler({{false}})">-</button>
  </view>
  <button @tap="broad">父组件通过broadcast广播告知子组件，子组件按级别依次响应</button>
  <comp id="comp" :num.sync="num"/>
  <ppppp />
  <view style="margin-top: 20rpx">
    <button @tap="invoke">直接调用另一个组件的方法，类似Vue通过refs获取实例调用方法</button>
  </view>
  <view style="margin-top: 20rpx">
    <button @tap="invoke2">同上，调用子组件中的子组件...</button>
  </view>
</template>

<script>
  import wepy from 'wepy'
  import comp from './../components/comp'
  import ppp from './../components/ppp'

  export default class Index extends wepy.page {
    config = {
      navigationBarTitleText: 'test'
    };
    components = {
      comp,
      ppppp: ppp
    };

    mixins = [];

    data = {
      userInfo: {},
      num: 10
    };

    computed = {

    };

    methods = {
      numHandler(flag) {
        flag ? this.num++ : this.num--;
      },
      broad() {
        this.$broadcast('jian');
      },
      invoke() {
        this.$invoke('comp', 'plus')
      },
      invoke2() {
        this.$invoke('comp/ppp', 'change')
      }
    };

    events = {
      plus() {
        this.num++;
      }
    };

    async onLoad() {

    }
  }
</script>
