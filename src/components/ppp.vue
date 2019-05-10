<template>
  <view style="text-align: center">
    <text>{{str}}</text>
  </view>
  <button @tap="invoke">invoke调用同级组件方法试试看呢</button>
</template>

<script>
  import wepy from 'wepy'

  export default class Comp extends wepy.component {
    data = {
      str: 'default str'
    };
    methods = {
      change() {
        this.str = 'change str';
        this.methods.print();
      },
      print() {
        console.log('fuck');
      },
      invoke() {
        this.$invoke('../comp', 'plus')
      }
    };
  }
</script>

<style>

</style>
