<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank">babel</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
    <div :style="{ width: '100%', height: '400px', border: '1px solid #aaa' }">
      <canvas id="test" class="canvas"></canvas>
      <div>
        <button @click="clear">清除</button>
        <button @click="save">保存</button>
      </div>
    </div>
  </div>
</template>

<script>
import SignaturePad from 'signature_pad'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      sig: () => {}
    }
  },
  methods: {
    draw () {
      let _this = this
      let canvas = document.getElementById('test')
      _this.sig = new SignaturePad(canvas, {
        backgroundColor:'rgb(255,255,255)',
				penColor : 'rgb(0, 0, 0)'
      })
      function resizeCanvas () {
        let ratio = Math.max(window.devicePixelRatio || 1, 1)
        canvas.width = canvas.offsetWidth * ratio
        canvas.height = canvas.offsetHeight * ratio
        canvas.getContext('2d').scale(ratio, ratio)
        _this.clear()
      }
      window.addEventListener('resize', resizeCanvas)
      resizeCanvas()
    },
    clear () {
      let _this = this
      _this.sig.clear()
    },
    save (format) {
      let _this = this
      let backData = format ? _this.sig.toDataURL(format) : _this.sig.toDataURL()
      console.log(backData)
    }
  },
  mounted () {
    let _this = this
    this.$nextTick(() => {
      _this.draw()
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.canvas {
  width: 100%;
  height: 100%;
}
</style>
