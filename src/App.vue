<template>
  <div id="app">
    <div class="box">
      <textarea v-model="text" class="before" placeholder="请输入多段文字"></textarea>
      <button @click="sendText">转换</button>
      <hr>
      <h4>以下是结果</h4>
      <textarea v-model="result" class="before"></textarea>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  components: {},
  data () {
    return {
      text: '',
      result: ''
    }
  },
  methods: {
    async sendText () {
      const sentences = this.text.split('\n')
      console.log(sentences)
      this.result = sentences.join('\n')
      const { data: result } = await axios.post('http://localhost:8081/text/upload', JSON.stringify(sentences), {
        headers: {
          'Content-Type': 'application/json;charset=UTF-8'
        }
      })
      this.result = result.join('\n')
    }
  }
}
</script>

<style lang="less" scoped>
.box {
  margin: auto;
  width: 500px;
  height: 900px;
  background-color: white;
  text-align: center;

  textarea {
    width: 400px;
    height: 250px;
    box-sizing: border-box;
    padding: 15px;
    border-radius: 25px;
    resize: none;
  }

  button {
    margin: 30px auto;
    width: 350px;
    height: 50px;
    border: 0;
    border-radius: 25px;
    background-color: skyblue;
  }
}
</style>
