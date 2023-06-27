<template>
  <div class="components-container">
    <aside><strong>SplitPane</strong> If you've used
      <a href="https://codepen.io/" target="_blank"> codepen</a>,
      <a href="https://jsfiddle.net/" target="_blank"> jsfiddle </a>will not be unfamiliar.
      <a href="https://github.com/PanJiaChen/vue-split-pane" target="_blank"> Github repository</a>
    </aside>
    <split-pane split="vertical" :max-percent="50" :default-percent="10" @resize="resize">
      <template slot="paneL">
        <div ref="stepBoxStyle" class="left-container" />
      </template>
      <template slot="paneR">
        <split-pane split="horizontal">
          <template slot="paneL">
            <div class="top-container" />
          </template>
          <template slot="paneR">
            <div class="bottom-container" />
          </template>
        </split-pane>
      </template>
    </split-pane>
  </div>
</template>

<script>
import splitPane from 'vue-splitpane'

export default {
  name: 'SplitpaneDemo',
  components: { splitPane },
  data() {
    return {
      minPercent: 20, // 往右拖动最小为15，往左最小为
      stepBoxWidth: null
    }
  },
  mounted() {
    // 记录左侧宽度
    this.stepBoxWidth = this.$refs.stepBoxStyle.clientWidth
  },
  methods: {
    resize() {
      this.$nextTick(() => {
        const newWidth = JSON.parse(JSON.stringify(this.$refs.stepBoxStyle.clientWidth))
        if (newWidth < this.stepBoxWidth) {
          this.minPercent = 20
        } else if (newWidth > this.stepBoxWidth) {
          this.minPercent = 30
        }
        console.log(newWidth, 'newWidth')
        console.log(this.minPercent, 'minPercent')
        this.stepBoxWidth = JSON.parse(JSON.stringify(newWidth))
      })
    }
  }
}
</script>

<style  scoped>
  .components-container {
    position: relative;
    height: 100vh;
  }

  .left-container {
    background-color: #F38181;
    height: 100%;
  }

  .right-container {
    background-color: #FCE38A;
    height: 200px;
  }

  .top-container {
    background-color: #FCE38A;
    width: 100%;
    height: 100%;
  }

  .bottom-container {
    width: 100%;
    background-color: #95E1D3;
    height: 100%;
  }
</style>
