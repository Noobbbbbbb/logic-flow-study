<template>
  <div class="flow-view">
    <ControlPanel :mouseDownHandle=mouseDownHandle  :addNode="handleAppend"/>
    <div id="container"></div>
  </div>
  <!-- <div class="control-panel">
    <el-button @click="handleAppend">创建节点</el-button>
  </div> -->
</template>
<script setup>
import LogicFlow from '@logicflow/core'
import { onMounted } from 'vue'
import ControlPanel from './ControlPanel.vue';
let lf
const data = {
  // 节点
  nodes: [
    {
      id: 50,
      type: 'rect',
      x: 100,
      y: 150,
      text: '你好'
    },
    {
      id: 21,
      type: 'circle',
      x: 300,
      y: 150
    }
  ],
  // 边
  edges: [
    {
      type: 'polyline',
      sourceNodeId: 50,
      targetNodeId: 21
    }
  ]
}

onMounted(() => {
  const dom = document.querySelector('#container')
  lf = new LogicFlow({
    // 容器设置
    container: dom,
    stopScrollGraph: true,
    // stopZoomGraph: true,
    // 画布配置
    width: dom.clientWidth,
    height: dom.clientHeight - 10,
    background: {
      color: '#F0F0F0'
    },
    grid: {
      type: 'dot',
      size: 20
    },
    // 工具配置
    textEdit: true,
    isSilentMode: false,
    edgeType: 'line',
    snapline: true,
    // 样式配置
    style: {
      rect: {
        radius: 6
      }
    }
  })

  lf.render(data)
})


// 点击新增节点
const handleAppend=()=>{
    lf.addNode({
        type: 'rect',
        x: 100,
        y: 100,
    });
}

// 拖拽新增节点
const mouseDownHandle = config => {
  lf.dnd.startDrag(config);
};
</script>
<style>

.flow-view{
  height: 100%;
  width: 100%;
  display: flex;
}
#container {
  flex:1;
  height: 100%;
}
/* .control-panel{
    position: absolute;
    top: 10px;
    right: 10px;
    width: 300px;
    height: 100px;
    padding: 10px;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 100;
} */
</style>
