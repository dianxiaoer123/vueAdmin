<template>
	<div class="dashboard-editor-container">

    <el-row :gutter="20">
      <el-col :span="6">
        <div class="grid-content bg-green">
          <i class="iconSet"></i>
            <div class="colBox">
               <div class="colname">当前设备总数</div>
               <div class="colcount">1985</div>
            </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-green">
          <i class="iconSet"></i>
          <div class="colBox">
            <div class="colname">今日设备新增数</div>
            <div class="colcount">0</div>
          </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-green">
          <i class="iconSet"></i>
          <div class="colBox">
            <div class="colname">当前设备故障数</div>
            <div class="colcount">0</div>
          </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-blue">
          <i class="iconUser"></i>
          <div class="colBox">
            <div class="colname">当前用户人数</div>
            <div class="colcount">1403</div>
          </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-blue">
          <i class="iconUser"></i>
          <div class="colBox">
            <div class="colname">昨日用户增长数</div>
            <div class="colcount">0%</div>
          </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-blue">
          <i class="iconUser"></i>
          <div class="colBox">
            <div class="colname">今日活跃用户数</div>
            <div class="colcount">373</div>
          </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-purple">
          <i class="iconList"></i>
          <div class="colBox">
            <div class="colname">今日订单数</div>
            <div class="colcount">33</div>
          </div>
        </div>
      </el-col>
      <el-col :span="6">
        <div class="grid-content bg-purple">
          <i class="iconList"></i>
          <div class="colBox">
            <div class="colname">本月订单数</div>
            <div class="colcount">1373</div>
          </div>
        </div>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="12">
        <linebar-chart></linebar-chart>
      </el-col>

      <el-col :span="12">
        <bar-chart></bar-chart>
      </el-col>
    </el-row>


    <el-row :gutter="20">
      <el-col :span="12">
        <line-chart></line-chart>
      </el-col>
    </el-row>
	</div>
</template>

<script>
import { mapGetters } from 'vuex'
import countTo from 'vue-count-to'
import panThumb from '@/components/PanThumb'
import todoList from '@/components/TodoList'
import pieChart from './pieChart'
import linebarChart from './linebarChart'
import lineChart from './lineChart'
import barChart from './barChart.vue'

export default {
  name: 'dashboard-admin',
  components: { countTo, panThumb, todoList, pieChart, lineChart, linebarChart, barChart },
  data() {
    return {
      statisticsData: {
        dayPickTotal: 0,
        daySuccessTotal: 0
      }
    }
  },
  created() {
    this.getList()
  },
  methods: {
    getList() {

    }
  },
  computed: {
    ...mapGetters([
      'name',
      'avatar',
      'roles'
    ])
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.dashboard-editor-container {
    margin: 30px;
    .btn-group {
        margin-bottom: 60px;
    }
    .box-card-header {
        position: relative;
        height: 160px;
    }
    .panThumb {
        z-index: 100;
        height: 150px;
        width: 150px;
        position: absolute;
        left: 0px;
        right: 0px;
        margin: auto;
    }
    .display_name{
        font-size: 30px;
        display: block;
    }
    .info-item{
        display: inline-block;
        margin-top: 10px;
        font-size: 14px;
        &:last-of-type{
            margin-left: 15px;
        }
    }

  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }

  .grid-content {
    border-radius: 4px;
    height:114px;
    margin-top: 20px;
    padding:27px;
    color:white;
    display: flex;
  }
  .grid-content i{
    display: block;
    width: 60px;
    height: 60px;
    margin-right: 25px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
  .colname{
    font-size: 14px;
    margin-top: 5px;
  }
  .colcount{
    font-size: 27px;
  }
  .el-row{
    margin-top: 50px;
  }
}
</style>
