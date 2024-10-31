<template>
  <div>
    <div class="header-Statistic">
      <el-row :gutter="20">
        <el-col :span="6">
          <div>
            <el-statistic
                title="合作单位数量"
                :value="value1">
              <template slot="prefix">
                <i class="el-icon-coffee-cup"></i>
              </template>
            </el-statistic>
          </div>
        </el-col>
        <el-col :span="6">
          <div>
            <el-statistic
                title="停车场数量"
                :value="value2">
              <template slot="prefix">
                <i class="el-icon-coffee-cup"></i>
              </template>
            </el-statistic>
          </div>
        </el-col>
        <el-col :span="6">
          <div>
            <el-statistic
                group-separator=","
                :value="value3"
                title="车辆数量">
              <template slot="prefix">
                <i class="el-icon-coffee-cup"></i>
              </template>
            </el-statistic>
          </div>
        </el-col>
        <el-col :span="6">
          <div>
            <el-statistic
                title="收益总额"
                :value="value4">
              <template slot="prefix">
                <i class="el-icon-coffee-cup"></i>
              </template>
            </el-statistic>
          </div>
        </el-col>
      </el-row>
    </div>
    <el-row>
      <div ref="chart1" style="width: 50%;height:400px;float: left"></div>
      <div ref="chart2" style="width: 50%;height:400px;float: right"></div>
    </el-row>
  </div>
</template>

<script>
import * as echarts from 'echarts';
export default {
  name: "consolepage",
  data(){
    return {
      value1: 2,
      value2: 1,
      value3: 1,
      value4: 10893,
    }
  },
  methods:{
    myEcharts1(){
      // 基于准备好的dom，初始化echarts实例
      const myChart = echarts.init(this.$refs['chart1']);

      // 指定图表的配置项和数据
      const option = {
        title: {
          text: '订单支付类型'
        },
        tooltip: {},
        legend: {
          data: ['支付额']
        },
        xAxis: {
          data: ['微信','支付宝','Apple Pay','HuaWei Pay']
        },
        yAxis: {},
        series: [
          {
            name: '支付额',
            type: 'bar',
            data: [85,55,35,25]
          }
        ]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    },
    myEcharts2(){
      // 基于准备好的dom，初始化echarts实例
      const myChart = echarts.init(this.$refs['chart2']);

      // 指定图表的配置项和数据
      const option = {
        title: {
          text:'最近七日支付订单'
        },
        xAxis: {
          type: 'category',
          data: ['06-01','06-02','06-03','06-04','06-05','06-06','06-07'],
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name:'数值',
            data: [120,200,150,204,388,245,125],
            type: 'line',
          }
        ]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    }
  },
  mounted() {
    this.myEcharts1()
    this.myEcharts2()
  }
}
</script>

<style scoped>
.header-Statistic{
  width: 100%;
  height: 100px;
  display: flex;
  align-items: center;
}
.el-row{
  width: 100%;
}
.el-statistic{
  font-size: 2.5rem;
  --borderWidth: 3px;
  position: relative;
  border-radius: var(--borderWidth);
}
.el-statistic:after{
  content: '';
  position: absolute;
  top: calc(-1 * var(--borderWidth));
  left: calc(-1 * var(--borderWidth));
  height: calc(100% + var(--borderWidth) * 2);
  width: calc(100% + var(--borderWidth) * 2);
  background: linear-gradient(60deg, #f79533, #f37055, #ef4e7b, #a166ab, #5073b8, #1098ad, #07b39b, #6fba82);
  border-radius: calc(2 * var(--borderWidth));
  z-index: -1;
  animation: animatedgradient 3s ease alternate infinite;
  background-size: 300% 300%;
}


</style>