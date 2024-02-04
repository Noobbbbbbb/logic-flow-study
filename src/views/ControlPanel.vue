<template>
    <div class="control-panel">
        <div class="control-panel-title">节点新增</div>
        <div>
            <div>点击新增</div>
            <el-button type="primary" @click="addNode">新增</el-button>
        </div>
        <div v-for="item in shapeList" :key="item.type">
            <div
                :class='[`panel-${type}`]'
                @mousedown='mouseDown(item)'
              >
              <span>{{ item.text }}</span>
            </div>
        </div>
    </div>
</template>
<script setup>

    const props = defineProps({
            mouseDownHandle: {
                type: Function,
                required: true
            },
            addNode: {
                type: Function,
                required: true
            }
        })
    const shapeList= [
        {
            type: 'rect',
            text: '矩形',
        },
        {
            type: 'circle',
            text: '圆形',
        },
    ]
    const mouseDown = ({ type, text })=>{
        const { mouseDownHandle } = props;
        mouseDownHandle({
            type,
            text,
        });
    }
</script>
<style scoped>
.control-panel{
    width: 200px;
    height: 100%;
    border-right: 1px solid lightgray;
}
.control-panel-title{
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 20px;
    font-weight: bold;
}
</style>