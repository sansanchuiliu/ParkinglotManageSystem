<!-- 合作单位 -->
<template>
    <div class="stop">
      <!-- 表头 -->
      <div class="hea">
        <div class="left">
          <el-input v-model="search" placeholder="请输入内容"></el-input>
          <el-button type="primary" icon="el-icon-search">搜索</el-button>
          <el-button type="primary" icon="el-icon-refresh">重置</el-button>
        </div>
        <el-button
          type="primary"
          icon="el-icon-plus"
          @click="dialogFormVisible = true"
          >新增</el-button
        >
        <el-dialog :visible.sync="dialogFormVisible">
          <el-form :model="form">
            <el-form-item label="序号" :label-width="formLabelWidth">
              <el-input v-model="form.id" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="单位代码" :label-width="formLabelWidth">
              <el-input v-model="form.unitcode" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="单位名称" :label-width="formLabelWidth">
              <el-input v-model="form.unitname" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="单位全称" :label-width="formLabelWidth">
              <el-input v-model="form.unitfullname" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="创建时间" :label-width="formLabelWidth">
              <el-input type="date" v-model="form.settime"></el-input>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible = false">取 消</el-button>
            <el-button type="primary" @click="addData">确 定</el-button>
          </div>
        </el-dialog>
      </div>
      <!-- 表格 -->
      <div>
        <el-table :data="tableData" border style="width: 100%">
          <el-table-column fixed prop="id" label="序号" width="150">
          </el-table-column>
          <el-table-column prop="unitcode" label="单位代码" width="150">
          </el-table-column>
          <el-table-column prop="unitname" label="单位名称" width="200">
          </el-table-column>
          <el-table-column prop="unitfullname" label="单位全称" width="200">
          </el-table-column>
          <el-table-column prop="settime" label="创建时间" width="200">
          </el-table-column>
          <el-table-column label="操作" width="300">
            <template slot-scope="scope">
              <el-button
                type="primary"
                icon="el-icon-edit"
                @click="editItem(scope.row)"
                >修改</el-button
              >
              <el-dialog :visible.sync="dialogFormVisible1">
                <el-form :model="form1">
                  <el-form-item label="序号" :label-width="formLabelWidth">
                    <el-input v-model="form1.id" autocomplete="off"></el-input>
                  </el-form-item>
                  <el-form-item label="单位代码" :label-width="formLabelWidth">
                    <el-input
                      v-model="form1.unitcode"
                      autocomplete="off"
                    ></el-input>
                  </el-form-item>
                  <el-form-item label="单位名称" :label-width="formLabelWidth">
                    <el-input
                      v-model="form1.unitname"
                      autocomplete="off"
                    ></el-input>
                  </el-form-item>
                  <el-form-item label="单位全称" :label-width="formLabelWidth">
                    <el-input
                      v-model="form1.unitfullname"
                      autocomplete="off"
                    ></el-input>
                  </el-form-item>
                  <el-form-item label="创建时间" :label-width="formLabelWidth">
                    <el-input type="date" v-model="form1.settime"></el-input>
                  </el-form-item>
                </el-form>
                <div slot="footer" class="dialog-footer">
                  <el-button @click="dialogFormVisible1 = false">取 消</el-button>
                  <el-button type="primary" @click="updateData()"
                    >确 定</el-button
                  >
                </div>
              </el-dialog>
              <el-button
                type="primary"
                icon="el-icon-delete"
                @click="handleDelete(scope.row)"
                >删除</el-button
              >
              <el-dialog
                :visible.sync="showDeleteDialog"
                width="30%"
                :before-close="handleClose"
              >
                <span>确定删除词条内容嘛？</span>
                <span slot="footer" class="dialog-footer">
                  <el-button @click="showDeleteDialog = false">取 消</el-button>
                  <el-button type="primary" @click="confirmDelete"
                    >确 定</el-button
                  >
                </span>
              </el-dialog>
            </template>
          </el-table-column>
        </el-table>
      </div>
      <!-- 页脚 -->
      <div>
        <el-pagination background layout="prev, pager, next" :total="40">
        </el-pagination>
      </div>
    </div>
  </template>
  <script>
  export default {
    data() {
      return {
        search: "",
        tableData: [
          {
            id: 1,
            unitcode: "154782",
            unitname: "青岛海信",
            unitfullname: "青岛海信有限公司",
            settime: "2021-09-28 12:00:00",
          },
        ],
        form: {
          id: "",
          unitcode: "",
          unitname: "",
          unitfullname: "",
          settime: "",
        },
        form1: {
          id: "",
          unitcode: "",
          unitname: "",
          unitfullname: "",
          settime: "",
        },
        dialogFormVisible: false,
        dialogFormVisible1: false,
        showDeleteDialog: false, // 控制弹窗的显示与隐藏
        deleteId: null, // 新增一个用于存储要删除的数据项ID的变量
      };
    },
    methods: {
      //新增功能
      // 显示对话框
      showDialog() {
        this.dialogFormVisible = true;
        this.resetForm(); // 重置表单数据（可选）
      },
      // 关闭对话框
      closeDialog() {
        this.dialogFormVisible = false;
        this.resetForm(); // 可选：在关闭对话框时重置表单数据
      },
      // 重置表单数据
      resetForm() {
        this.form = {
          id: "",
          affiliation: "",
          stopname: "",
          carnumber: "",
          carname: "",
          gender: "",
          state: "",
          label: "",
          settime: "",
        };
      },
      // 新增数据
      addData() {
        // 在这里你可以进行数据的验证或处理
        // 假设验证通过，将数据添加到dataList中
        this.tableData.push({ ...this.form }); // 使用展开运算符复制表单数据
        // 关闭对话框
        this.closeDialog();
        // 你可以在这里发送请求到服务器保存数据（异步操作）
      },
      //删除功能
      handleClose(done) {
        this.$confirm("确认关闭？")
          .then((_) => {
            done();
          })
          .catch((_) => {});
      },
      handleDelete(row) {
        this.deleteId = row.id; // 保存要删除的数据项ID
        this.showDeleteDialog = true; // 显示对话框
      },
      confirmDelete() {
        // 根据 deleteId 找到对应的数据项并删除它
        this.tableData = this.tableData.filter(
          (item) => item.id !== this.deleteId
        );
        this.showDeleteDialog = false; // 关闭对话框
        this.deleteId = null; // 清空 deleteId
      },
      //修改功能
      editItem(row) {
        this.editingItem = row; // 存储要编辑的数据项
        this.form1 = { ...this.editingItem }; // 预填充表单
        this.dialogFormVisible1 = true; // 显示对话框
      },
      updateData() {
        const index = this.tableData.findIndex(
          (item) => item.id === this.editingItem.id
        );
        if (index !== -1) {
          // 更新原始数据列表中的对应项
          this.tableData.splice(index, 1, this.form1);
          // 关闭对话框
          this.dialogFormVisible1 = false;
        }
      },
    },
  };
  </script>
  <style>
  .stop {
    height: 86%;
    background-color: #ffff;
  }
  .hea {
    width: 100%;
    height: 50px;
    margin-bottom: 2%;
    padding: 0 30px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .hea > .left {
    display: flex;
    align-items: center;
  }
  .hea > .left > .el-input {
    margin-right: 20px;
  }
  .cell {
    display: flex;
    align-items: center;
  }
  .el-table {
    margin-bottom: 30px;
  }
  </style>