<template>
  <div @keydown="keydown">
    <div class="text-center span-content">
      <span v-for="letter in letter1" :id="letter" :key="letter" :class="{'press-down':letter===currentKey}">
        {{letter}}
      </span>
    </div>
    <div class="text-center span-content">
      <span v-for="letter in letter2" :id="letter" :key="letter" :class="{'press-down':letter===currentKey}">
        {{letter}}
      </span>
    </div>
    <div class="text-center span-content">
      <span v-for="letter in letter3" :id="letter" :key="letter" :class="{'press-down':letter===currentKey}">
        {{letter}}
      </span>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      letter1:['Q','W','E','R','T','Y','U','I','O','P'],
      letter2:['A','S','D','F','G','H','J','K','L'],
      letter3:['Z','X','C','V','B','N','M',],
      currentKey:'',
    }
  },
  created() {
    document.body.addEventListener('keydown',this.keydown)
    document.body.addEventListener('keyup',this.keyup)
  },
  methods:{
    keydown(e) {
      this.currentKey = e.key.toUpperCase()
    },
    keyup() {
      this.currentKey = ''
    },
    sound() {
      const synth = window.speechSynthesis; // 启用文本
      const msg = new SpeechSynthesisUtterance(); // 表示一次发音请求。其中包含了将由语音服务朗读的内容，以及如何朗读它（例如：语种、音高、音量）。

      // 语音播报的函数
      const handleSpeak=(text,lang)=> {
        msg.text = text; // 文字内容: 测试内容
        msg.lang = lang?lang:"en-US"; // 使用的语言:中文 en-US、zh-CN
        msg.volume = 1; // 声音音量：1
        msg.rate = 1; // 语速：1
        msg.pitch = 1; // 音高：1
        synth.speak(msg); // 播放
      }
      // 语音停止
      // const  handleStop=(e)=>  {
      //   msg.text = e;
      //   msg.lang = "en-US";
      //   synth.cancel(msg); // 取消该次语音播放
      // }

      handleSpeak("hello")
    }
  }
}
</script>
<style lang="less">
@import './assets/css/styles.less';
.span-content span{
  font-size: 36px;
  padding: 10px;
  margin-right: 10px;
  margin-bottom: 15px;
  border: 1px solid #c6c6c6;
  border-radius: 8px;
  line-height: 1.5em;
  width: 40px;
  display: inline-block;
}
.press-down {
  box-shadow: 0px 0px 8px red;
}
@media screen and (max-width: 780px){
  .span-content span{
    font-size: 24px !important;
    width: 28px !important;
  }
}
@media screen and (max-width: 660px){
  .span-content span{
    font-size: 20px !important;
    width: 20px !important;
  }
}
</style>
