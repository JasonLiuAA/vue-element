<!--
 * @Author: 刘家辰
 * @Date: 2020-08-11 12:18:29
 * @LastEditTime: 2020-08-11 12:33:07
 * @LastEditors: 刘家辰
 * @Description: tabel demo 
-->
<template>
  <div>
    <xtable
      :loadData="getGoods"
      :column="column"
      ref="adminList"
      :childrenData="getAllCat"
      :select="fun"
      :single="true"
    >
      <template v-slot:cover="{ scope }">
        <el-image :src="scope.cover" class="admin_avater" :preview-src-list="[scope.cover]" />
      </template>
      <template v-slot:miniQrCodeLink="{ scope }">
        <el-image
          :src="scope.miniQrCodeLink"
          class="admin_avater"
          :preview-src-list="[scope.miniQrCodeLink]"
        />
      </template>
      <template v-slot:putOn="{ scope }">
        <el-switch
          v-model.trim="scope.putOn"
          active-color="#13ce66"
          inactive-color="#ff4949"
          @change="putOnGoods(scope.id)"
        ></el-switch>
      </template>
      <template v-slot:newFlag="{ scope }">
        <el-switch
          v-model.trim="scope.newFlag"
          active-color="#13ce66"
          inactive-color="#ff4949"
          @change="newFlagGoods(scope.id)"
        ></el-switch>
      </template>
    </xtable>
  </div>
</template>

<script>
import xtable from "./index";
export default {
  components: {
    xtable,
  },
  data() {
    return {
      column: [
        {
          prop: "createTime",
          label: "创建时间",
          formatter: (row, column) => {
            return parseTime(row.createTime);
          },
        },
        {
          prop: "cover",
          label: "商品图片",
          render: true,
        },
        {
          prop: "name",
          label: "商品名称",
        },
        {
          prop: "id",
          label: "商品编码",
        },
        {
          prop: "catName",
          label: "品类",
          formatter: (row, column) => {
            return `${row.parentCatName}-${row.catName}`;
          },
        },
        {
          prop: "supplierName",
          label: "供应商",
        },
        {
          prop: "brandName",
          label: "品牌",
        },
        {
          prop: "stock",
          label: "库存",
        },
        {
          prop: "saleCount",
          label: "累计销量",
        },
        {
          prop: "miniQrCodeLink",
          label: "小程序二维码",
          render: true,
        },
        {
          prop: "putOn",
          label: "上/下架",
          render: true,
        },
        {
          prop: "newFlag",
          label: "上新",
          render: true,
        },
        {
          prop: "actives",
          label: "操作",
          actives: [
            {
              name: "查看",
              method: (val) => {},
            },
            {
              name: "编辑",
              method: (val) => {},
            },
            {
              name: (val) => {
                //   控制按钮是否显示
                val.show = true;
                if (val.show) {
                  return "显示";
                } else {
                  return false;
                }
              },
              method: (val) => {},
            },
          ],
        },
      ],
    };
  },
  computed: {
    //获取数据接口  必须要放在计算属性中 否则表格操作后不会更新
    getGoods() {
      return getGoods;
    },
  },
  methods: {
    //   重置表格
    reset() {
      this.$refs.adminList.reset();
    },
    // 搜索并更新表格 this.searchfrom为搜索参数
    search() {
      this.$refs.adminList.update({ ...this.searchfrom });
    },
    // 单选/多选  single为true时为单选
    fun(val) {
      console.log(val);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
