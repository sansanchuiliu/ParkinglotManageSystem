/** *@description: *@author: YuChen Zhang *@date: 2024-06-05 */ // 停车场管理
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
          @click="goAdd"
          >新增</el-button
        >
      </div>
    </div>
    <div>
      <template>
        <el-table :data="tableData" style="width: 100%">
          <el-table-column prop="id" label="序号" width="100">
          </el-table-column>
          <el-table-column prop="stopName" label="停车场名称" width="120">
          </el-table-column>
          <el-table-column prop="num" label="车位总数" width="100">
          </el-table-column>
          <el-table-column prop="time" label="免费时长" width="100">
          </el-table-column>
          <el-table-column prop="date" label="计时单元" width="100">
          </el-table-column>
          <el-table-column prop="money" label="单元费用" width="100">
          </el-table-column>
          <el-table-column prop="setDate" label="创建时间" width="200">
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
            <el-button
              type="primary"
              icon="el-icon-bank-card"
              size="small"
              @click="test"
              plain
              >支付配置</el-button
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
          stopName: "万达停车场",
          num: 12,
          time: "15",
          date: "30",
          money: "2.00",
          setDate: "2024-05-27 21:52:08",
        },
      ],
      currentPage: 1,
    };
  },
  methods: {
    goAdd() {
      this.$router.push("/addStop");
    },
    goEdit() {
      this.$router.push("/editStop");
    },
    test() {
      this.$router.push("/paySetting");
    },
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
