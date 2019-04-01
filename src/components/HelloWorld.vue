<template>
  <div class="hello">
    <div class="tip">pc端请使用移动端模拟或使用移动端打开</div>
    <div class="tipText">{{text}}</div>
    <gesture-lock :containerWidth="width"
                  :cycleRadius="30"
                  @end="onEnd"
                  :password="password"></gesture-lock>
  </div>
</template>

<script>
import GestureLock from '@/components/GestureLock/gestureLock';
export default {
  name: 'HelloWorld',
  components: {
    GestureLock
  },
  data () {
    return {
      title: "手势图案",
      password: [],
      text: '请设定手势',
    }
  },
  computed: {
    width () {
      return window.innerWidth
    }
  },
  methods: {
    onEnd (data) {
      if (this.password.length) {
        if (this.password.join('') === data.join('')) {
          this.text = '手势设定完成'
          window.alert("你的密码是" + this.password)
          this.password = []
        } else {
          this.text = '两次手势设定不一致'
          this.password = []
        }
      } else {
        this.text = '请确认手势设定'
        this.password = data
      }
    }
  },
  mounted () {

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.tip {
  color: red;
  margin-bottom: 20px;
}
</style>
