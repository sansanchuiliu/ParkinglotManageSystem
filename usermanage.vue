/** *@description: *@author: YuChen Zhang *@date: 2024-06-12 */
<template>
  <div>
    <div class="top">
      <div class="left">
        <el-input
          v-model="search"
          placeholder="请输入搜索按钮"
          size="normal"
          clearable
          @change=""
        ></el-input>
        <el-button type="primary" icon="el-icon-search" size="default" @click=""
          >搜索</el-button
        >
        <el-button type="primary" size="default" @click="">重置</el-button>
      </div>
      <div class="right">
        <el-button
          type="primary"
          icon="el-icon-plus"
          size="default"
          @click="dialogFormVisible = true"
          >新增</el-button
        >
        <el-dialog title="新增用户" :visible.sync="dialogFormVisible">
          <el-form :model="form">
            <el-form-item label="用户名" :label-width="formLabelWidth">
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="密码" :label-width="formLabelWidth">
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="邮箱" :label-width="formLabelWidth">
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="电话" :label-width="formLabelWidth">
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="角色" :label-width="formLabelWidth">
              <el-select v-model="form.region" placeholder="请选择角色">
                <el-option label="管理员" value="shanghai"></el-option>
                <el-option label="非管理员" value="beijing"></el-option>
              </el-select>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible = false">取 消</el-button>
            <el-button type="primary" @click="dialogFormVisible = false"
              >确 定</el-button
            >
          </div>
        </el-dialog>
      </div>
    </div>
    <div>
      <template>
        <el-table :data="tableData" stripe style="width: 100%">
          <el-table-column prop="id" label="序号" width="50"> </el-table-column>
          <el-table-column prop="userRole" label="角色标识" width="100">
          </el-table-column>
          <el-table-column prop="userName" label="角色名称" width="120">
          </el-table-column>
          <el-table-column prop="email" label="邮箱" width="200">
          </el-table-column>
          <el-table-column prop="phone" label="手机号" width="200">
          </el-table-column>
          <el-table-column prop="" label="操作" width="">
            <el-button
              type="primary"
              icon="el-icon-edit"
              size="small"
              @click="goEdit"
              plain
              >修改</el-button
            >
            <el-button
              type="primary"
              icon="el-icon-delete"
              size="small"
              @click="test"
              plain
              >删除</el-button
            >
          </el-table-column>
        </el-table>
      </template>
    </div>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="currentPage"
      :page-sizes="[5, 8, 10, 20]"
      :page-size="5"
      layout="total, sizes, prev, pager, next, jumper"
      :total="20"
    >
    </el-pagination>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          id: "1",
          userRole: "admin",
          userName: "角色名称",
          email: "222222222@qq.com",
          phone: "15255554444",
          time: "2024-05-25 12:00:00",
        },
      ],
      currentPage: 1,
      gridData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
        },
      ],
      dialogTableVisible: false,
      dialogFormVisible: false,
      form: {
        name: "",
        region: "",
        date1: "",
        date2: "",
        delivery: false,
        type: [],
        resource: "",
        desc: "",
      },
      formLabelWidth: "120px",
    };
  },
};
</script>

<style>
.top {
  width: 100%;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
  margin-top: 10px;
}
.left {
  display: flex;
  align-items: center;
  margin-left: 20px;
}
.left {
  margin: 10px;
}
.right {
  margin-right: 40px;
}
</style>
