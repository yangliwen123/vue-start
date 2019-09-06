<template>
  <div>
    <!--第一步 定义显示内容-->
    <el-table
      :key="getChange"
      :data="tableData"
      border
      style="width: 100%"
    >
      <el-table-column
        fixed
        prop="date"
        label="日期"
        width="150"
      />
      <el-table-column
        prop="name"
        label="姓名"
        width="120"
      />
      <el-table-column
        prop="province"
        label="省份"
        width="120"
      />
      <el-table-column
        prop="city"
        label="市区"
        width="120"
      />
      <el-table-column
        prop="address"
        label="地址"
        width="300"
      />
      <el-table-column
        prop="zip"
        label="邮编"
        width="120"
      />
      <el-table-column
        fixed="right"
        label="操作"
        width="100"
      >
        <template slot-scope="scope">
          <el-button type="text" size="small" plain @click="dialogOpen(scope.$index, scope.row)">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="更改" :visible.sync="dialogFormVisible">
      <el-form ref="formVisible" :model="form" class="custom-form">
        <el-form-item label="姓名" :label-width="formLabelWidth">
          <el-input v-model="form.name" auto-complete="off" />
        </el-form-item>
        <el-form-item label="地址" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择活动区域">
            <el-option label="区域一" value="shanghai" />
            <el-option label="区域二" value="beijing" />
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogClose()">取 消</el-button>
        <el-button type="primary" @click="confirm()">确 定</el-button>
      </div>
    </el-dialog>
    <!-- 第三步 使用组件-->
    <edit :dialog-visible="tableData" @call-back="callBack" />
    <div>documentation</div>
    <div>
      <el-button @click="dialogVisible = true">打开对话框</el-button>
      <edit :visible.sync="dialogVisible" @closeIt="closeIt()" />
    </div>
  </div>
</template>
//第二部 定义显示内容及显示内容绑定
<script>
// 第一步 导入文件；
import edit from '../edit.vue'
export default {
  components: {// 第二v步 注册组件
    edit
  },
  data() {
    return {
      formLabelWidth: '120px',
      dialogFormVisible: false,
      dialogVisible: false,
      getChange: 0,
      curIndex: 0,
      tableData: [{
        date: '2016-05-03',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-02',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-04',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }, {
        date: '2016-05-01',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
        zip: 200333
      }],
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: 'false',
        type: [],
        resource: '',
        desc: ''
      }
    }
  },
  // 第三步 定义交互方法并和显示内容事件建立绑定
  methods: {
    // 打开对话框
    dialogOpen(index, row) {
      this.curIndex = index
      this.form.name = row.name
      // 把当前的row值给对话框对应的name
      this.dialogFormVisible = true
      console.log(row, this.form)
    },
    // 关闭对话框
    dialogClose() {
      console.log('dialogClose before', this.dialogFormVisible)
      this.dialogFormVisible = false
      console.log('dialogClose after', this.dialogFormVisible)
    },
    confirm() {
      this.tableData[this.curIndex].name = this.form.name
      this.getChange = Math.random()
      console.log('confirm', this.tableData, this.curIndex, this.form.name)
      this.dialogFormVisible = false
    },
    callBack(params) {
      console.log('callBack', params)
    },
    closeIt() {
      this.dialogVisible = false
    }
  }
}
</script>
