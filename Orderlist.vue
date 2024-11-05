/** *@description: *@author: YuChen Zhang *@date: 2024-06-06 */
<template>
  <div>
    <div class="left">
      <el-select v-model="value1" multiple placeholder="请选择合作单位">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>

      <el-select
        v-model="value2"
        multiple
        collapse-tags
        placeholder="请选择停车场"
      >
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
      <el-input v-model="search" placeholder="请输入内容"></el-input>
      <el-button type="primary" icon="el-icon-search">搜索</el-button>
      <el-button type="primary" icon="el-icon-refresh-left">重置</el-button>
    </div>
    <template>
      <el-table :data="tableData" stripe style="width: 100%">
        <el-table-column prop="id" label="序号" width="50"> </el-table-column>
        <el-table-column prop="no" label="订单号" width="80"> </el-table-column>
        <el-table-column prop="cost" label="付款金额" width="100">
        </el-table-column>
        <el-table-column prop="num" label="车牌号" width="100">
        </el-table-column>
        <el-table-column prop="types" label="支付类型" width="100">
        </el-table-column>
        <el-table-column prop="createData" label="创建时间" width="200">
        </el-table-column>
        <el-table-column prop="overData" label="有效期至" width="200">
        </el-table-column>
        <el-table-column prop="detail" label="备注"> </el-table-column>
      </el-table>
    </template>
    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[10, 20, 30, 40]"
        :page-size="10"
        background
        layout="total, prev, pager, next, sizes, jumper"
        :total="1"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          id: "1",
          no: "145656",
          cost: "30.00",
          num: "124322",
          types: "微信支付",
          createData: "2024-05-22 12:00:00",
          overData: "2024-07-23 12:00:00",
          detail: "",
        },
      ],
    };
  },
};
</script>

<style>
.left {
  width: 50%;
}
.el-input__inner {
  width: 150px;
}
</style>
