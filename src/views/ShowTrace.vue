<template>
<div class="traceList">
  <row>
    <div class="trace">
      <el-button @click="visible = true">Button</el-button>
      <el-dialog :visible.sync="visible" title="Hello world">
        <p>Try Element</p>
      </el-dialog>
      <div id="trace1" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace2" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace3" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace4" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace5" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace6" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace7" style="width: 95%;height:800px; alignment: center"></div>
      <div id="trace8" style="width: 95%;height:800px; alignment: center"></div>
    </div>
  </row>

</div>
</template>
<!--<script src="../common/echarts.js"></script>-->
<script >
import echarts from 'echarts'
import treeJson from '../data/tree/tree.json'
import traceJson from '../data/trace.json'
export default {
  name: "ShowTrace",
  mounted() {
    this.init();
  },
  methods:{
    init()
    {
      var jsonName;
      var option;
      var trace;
      var traceChart;
      var title=Object.keys(traceJson);
      for (let i = 1; i <= 8; i++) {
        jsonName="trace"+i;
        trace=document.getElementById(jsonName)
        traceChart=echarts.init(trace)
        traceChart.setOption(
            (option = {
              title : {
                show:true, //显示策略，默认值true,可选为：true（显示） | false（隐藏）
                text: title[i-1], //主标题文本，'\n'指定换行
                link:'', //主标题文本超链接,默认值true
                target: null, //指定窗口打开主标题超链接，支持'self' | 'blank'，不指定等同为'blank'（新窗口）
                x:'center', //水平安放位置，默认为'left'，可选为：'center' | 'left' | 'right' | {number}（x坐标，单位px）
                y: 'top', //垂直安放位置，默认为top，可选为：'top' | 'bottom' | 'center' | {number}（y坐标，单位px）
                textAlign: null ,//水平对齐方式，默认根据x设置自动调整，可选为： left' | 'right' | 'center
                backgroundColor: 'rgba(0,0,0,0)', //标题背景颜色，默认'rgba(0,0,0,0)'透明
                borderColor: '#ccc', //标题边框颜色,默认'#ccc'
                borderWidth: 0, //标题边框线宽，单位px，默认为0（无边框）
                padding: 5, //标题内边距，单位px，默认各方向内边距为5，接受数组分别设定上右下左边距
                itemGap: 10, //主副标题纵向间隔，单位px，默认为10
                textStyle: { //主标题文本样式{"fontSize": 18,"fontWeight": "bolder","color": "#333"}
                  fontFamily: 'Arial, Verdana, sans...',
                  fontSize: 26,
                  fontStyle: 'normal',
                  fontWeight: 'normal',
                }},
              tooltip: {
                trigger: 'item',
                formatter: function(arg) {
                  let label=' name: '+arg.data['name']+'\navg: '+arg.data['avg']+'\nstd: '+arg.data['std']
                  return label
                },
                extraCssText:'width:600px; white-space:pre-wrap',
                triggerOn: 'mousemove'
              },
              series: [
                {
                  type: 'tree',

                  data: [treeJson[i-1]],
                  left: '2%',
                  right: '2%',
                  top: '8%',
                  bottom: '20%',
                  symbol: 'emptyCircle',
                  orient: 'vertical',
                  expandAndCollapse: true,
                  label: {
                    position: 'top',
                    rotate: 10,
                    verticalAlign: 'middle',
                    align: 'center',
                    fontSize: 15
                  },
                  leaves: {
                    label: {
                      position: 'bottom',
                      rotate: 10,
                      verticalAlign: 'middle',
                      align: 'center'
                    }
                  },
                  animationDurationUpdate: 750
                }
              ]
            })
        );
      }

    }
  }
}


</script>

<style scoped>



</style>