<template>
  <div class="app-container calendar-list-container">
    <div class="selectBox">
      <el-select v-model="value1" placeholder="设备MAC">
        <el-option
          v-for="item in options1"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          :disabled="item.disabled">
        </el-option>
      </el-select>

      <el-select v-model="value2" placeholder="设备状态">
        <el-option
          v-for="item in options2"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          :disabled="item.disabled">
        </el-option>
      </el-select>

      <el-select v-model="value3" placeholder="在线状态">
        <el-option
          v-for="item in options3"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          :disabled="item.disabled">
        </el-option>
      </el-select>
    </div>

    <div class="filter-container">
      <el-input @keyup.enter.native="handleFilter" style="width: 200px;" class="filter-item" v-model="listQuery.mac">
      </el-input>
      <el-button class="filter-item" type="primary" v-waves icon="search" @click="handleFilter">查询</el-button>
      <el-button class="filter-item" type="primary" style="margin-left: 0px;">重置</el-button>
    </div>

    <div class="findBox">
      <el-button-group>
        <el-button type="primary"><i class="el-icon-circle-check"></i>分配</el-button>
        <el-button type="primary"><i class="el-icon-circle-close"></i>解绑</el-button>
        <el-button type="primary"><i class="el-icon-d-caret"></i>导出</el-button>
        <el-button type="primary"><i class="el-icon-document"></i>自定义</el-button>
        <el-button type="primary"><i class="el-icon-upload2"></i>导入</el-button>
        <el-button type="primary"><i class="el-icon-plus"></i>添加</el-button>
        <el-button type="primary"><i class="el-icon-delete"></i>删除</el-button>
      </el-button-group>
    </div>

    <el-table :data="list" v-loading="listLoading" element-loading-text="加载中" border fit highlight-current-row
              style="width: 100%">
      <el-table-column
        type="selection">
      </el-table-column>

      <el-table-column min-width="100px" label="Id">
        <template scope="scope">
          <span>{{scope.row.id}}</span>
        </template>
      </el-table-column>

      <el-table-column min-width="200px" label="设备id">
        <template scope="scope">
          <span>{{scope.row.deviceId}}</span>
        </template>
      </el-table-column>
      <el-table-column min-width="200px" label="设备名称">
        <template scope="scope">
          <span>{{scope.row.name}}</span>
        </template>
      </el-table-column>
      <el-table-column min-width="100px" label="设备mac">
        <template scope="scope">
          <span>{{scope.row.mac}}</span>
        </template>
      </el-table-column>
      <el-table-column min-width="100px" label="绑定状态">
        <template scope="scope">
          <span>{{scope.row.bindStatus}}</span>
        </template>
      </el-table-column>
      <el-table-column align="left" label="操作">
        <template scope="scope">
          <el-button size="small" type="success" @click="handleUpdate(scope.row)">编辑
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog :title="textMap[dialogStatus]" :visible.sync="dialogFormVisible" size="large">
      <el-form class="small-space" :model="temp" label-position="left" label-width="120px">
        <el-form-item label="mac地址:">
         <span>{{temp.mac}}</span>
        </el-form-item>
        <el-form-item label="设备名称:">
          <el-input v-model="temp.name"></el-input>
        </el-form-item>
        <el-form-item label="添加时间:">
          <span>{{temp.mac}}</span>
        </el-form-item>
        <el-form-item label="设备序列号:">
          <span>{{temp.mac}}</span>
        </el-form-item>
        <el-form-item label="设备状态:">
          <span>空闲</span>
        </el-form-item>
        <el-form-item label="在线状态:">
          <span>离线</span>
        </el-form-item>
        <el-form-item label="所属产品:">
          <span>HK_YFS027_IFRE</span>
        </el-form-item>
        <el-form-item label="最后上线时间:">
          <span>2018-05-12 16:17:55</span>
        </el-form-item>

        <el-tabs v-model="activeName">
          <el-tab-pane label="运营信息" name="first">
            <el-form-item label="收费名称:">
              <el-input v-model="temp.name"></el-input>
            </el-form-item>
            <el-form-item label="投放点名称:">
              <el-input v-model="temp.name"></el-input>
            </el-form-item>
            <el-form-item label="设备二维码:">

            </el-form-item>

            <el-form-item label="收费类型:">
              <span>HK_YFS027_IFRE</span>
            </el-form-item>

            <el-form-item label="投放点地址:">
              <span>HK_YFS027_IFRE</span>
            </el-form-item>

            <el-form-item label="收费价格:">
              <span>HK_YFS027_IFRE</span>
            </el-form-item>

            <el-form-item label="投放点负责人:">
              <span>HK_YFS027_IFRE</span>
            </el-form-item>

            <el-form-item label="当前归属:">
              <span>HK_YFS027_IFRE</span>
            </el-form-item>

            <el-form-item label="负责人联系电话:">
              <span>HK_YFS027_IFRE</span>
            </el-form-item>
          </el-tab-pane>

          <el-tab-pane label="设备控制" name="second">
            <el-form-item label="开关机:">
              <el-switch
                v-model="svalue1"
                on-text=""
                off-text="">
              </el-switch>
            </el-form-item>

            <el-form-item label="启用/禁用:">
              <el-switch
                v-model="svalue2"
                on-text=""
                off-text="">
              </el-switch>
            </el-form-item>

            <el-form-item label="时长:">
              <el-input></el-input>
            </el-form-item>
          </el-tab-pane>
          <el-tab-pane label="订单列表" name="third">
              <el-table
                :data="tableDataList"
                border
                style="width: 100%">
                <el-table-column
                  prop="date"
                  label="订单号"
                  width="180">
                </el-table-column>
                <el-table-column
                  prop="name"
                  label="用户昵称"
                  width="180">
                </el-table-column>
                <el-table-column label="投放点">
                </el-table-column>
                <el-table-column label="设备Mac">
                </el-table-column>
                <el-table-column label="支付费用">
                </el-table-column>
                <el-table-column label="支付时间">
                </el-table-column>
                <el-table-column label="支付类型">
                </el-table-column>
                <el-table-column label="收费名称">
                </el-table-column>
                <el-table-column label="订单状态">
                </el-table-column>
                <el-table-column label="操作">
                </el-table-column>
              </el-table>
              <div style="margin-top: 10px;text-align: center;">
                <el-pagination
                  @size-change="handleSizeChange1"
                  @current-change="handleCurrentChange1"
                  :current-page="currentPage"
                  :page-sizes="[100, 200, 300, 400]"
                  :page-size="100"
                  layout="total, sizes, prev, pager, next, jumper"
                  :total="400">
                </el-pagination>
              </div>
          </el-tab-pane>
          <el-tab-pane label="运行日志" name="fourth">
            <el-table
              :data="tableDataList"
              border
              style="width: 100%">
              <el-table-column
                prop="date"
                label="设备状态">
              </el-table-column>
              <el-table-column
                prop="name"
                label="发生时间">
              </el-table-column>
              <el-table-column label="报文">
              </el-table-column>
            </el-table>
            <div style="margin-top: 10px;text-align: center;">
              <el-pagination
                @size-change="handleSizeChange1"
                @current-change="handleCurrentChange1"
                :current-page="currentPage"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </div>
          </el-tab-pane>
          <el-tab-pane label="操作记录" name="five">
            <el-table
              :data="tableDataList"
              border
              style="width: 100%">
              <el-table-column
                prop="date"
                label="用户名">
              </el-table-column>
              <el-table-column
                prop="name"
                label="操作内容">
              </el-table-column>
              <el-table-column label="访问ip地址">
              </el-table-column>
              <el-table-column label="操作时间">
              </el-table-column>

            </el-table>
            <div style="margin-top: 10px;text-align: center;">
              <el-pagination
                @size-change="handleSizeChange1"
                @current-change="handleCurrentChange1"
                :current-page="currentPage"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
              </el-pagination>
            </div>
          </el-tab-pane>
        </el-tabs>
      </el-form>



      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button  type="primary" @click="updateData">确 定</el-button>
      </div>
    </el-dialog>
    <div class="pagination-container">
      <el-pagination background @size-change="handleSizeChange" @current-change="handleCurrentChange"
                     :current-page="listQuery.page" :page-sizes="[10,20,30, 50]"
                     :page-size="listQuery.limit"
                     layout="total, sizes, prev, pager, next, jumper" :total="total">
      </el-pagination>
    </div>

  </div>
</template>

<script>
  import { queryDeviceList, queryDeviceCount, updateDevice } from '@/api/device'
  import waves from '@/directive/waves' // 水波纹指令

  export default {
    name: 'complexTable',
    directives: {
      waves
    },
    data() {
      return {
        currentPage:1,
        tableDataList: [{
          date: '123456',
          name: '小王',
        }],
        svalue1:false,
        svalue2:false,
        activeName: 'first',
        options1: [{
          value: '设备MAC',
          label: ''
        }, {
          value: '设备序列号',
          label: '设备序列号',
        }, {
          value: '设备名称',
          label: '设备名称'
        }, {
          value: '投放点',
          label: '投放点'
        }],
        value1: '',
        options2: [{
          value: '设备状态',
          label: ''
        }, {
          value: '使用中',
          label: '使用中',
        }, {
          value: '空闲',
          label: '空闲'
        }, {
          value: '障碍',
          label: '障碍'
        }],
        value2: '',
        options3: [{
          value: '在线状态',
          label: ''
        }, {
          value: '在线',
          label: '在线',
        }, {
          value: '离线',
          label: '离线'
        }],
        value3: '',
        list: null,
        total: null,
        listLoading: true,
        listQuery: {
          page: 1,
          limit: 50,
          mac: undefined
        },
        temp: {
          id: undefined,
          name: ''
        },
        dialogFormVisible: false,
        dialogStatus: '',
        textMap: {
          update: '编辑',
          create: '创建'
        }
      }
    },
    created() {
      this.getList()
    },
    methods: {
      handleSizeChange1(){},
      handleCurrentChange1(){},
      getList() {
        this.listLoading = true
        queryDeviceCount(this.listQuery).then(response => {
          this.total = response.data.data
        })
        queryDeviceList(this.listQuery).then(response => {
          this.list = response.data.data
          this.listLoading = false
        })
      },
      handleFilter() {
        this.listQuery.page = 1
        this.getList()
      },
      handleSizeChange(val) {
        this.listQuery.limit = val
        this.getList()
      },
      handleCurrentChange(val) {
        this.listQuery.page = val
        this.getList()
      },
      resetTemp() {
        this.temp = {
          id: undefined,
          mac: ''
        }
      },
      handleCreate() {
        this.resetTemp()
        this.dialogStatus = 'create'
        this.dialogFormVisible = true
      },
      createData() {
      },
      handleUpdate(row) {
        this.temp = {
          id: row.id,
          mac: row.mac,
          name: row.name
        }
        this.dialogStatus = 'update'
        this.dialogFormVisible = true
      },
      updateData() {
        const tempData = Object.assign({}, this.temp)
        updateDevice(tempData).then(() => {
          this.handleFilter()
          this.$notify({
            title: '成功',
            message: '更新成功',
            type: 'success',
            duration: 2000
          })
        })
      }
    }
  }
</script>

<style scoped>
  .el-form-item .el-input{
    width: 300px;
  }
  .selectBox{
    margin-bottom: 10px;
  }
.findBox{
  margin-top: 5px;
  margin-bottom: 10px;
  text-align: right;
}
  .el-button i{
    margin-right: 5px;
  }
</style>
