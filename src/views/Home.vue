<template>
    <el-container style="min-height: 100vh;">
      <el-aside :width="dtwidth+'px'" style="background-color: rgb(238, 241, 246);min-height: 100vh;background-color: rgb(48 65 86)">
        <el-menu :default-openeds="['1', '3']" height="100%"  background-color="rgb(48 65 86)"
        text-color="#fff"  style="overflow-x: hidden" active-text-color="#4ec51d"
                 :collapse="isCollapse"
                 :collapse-transition="false" class="el-menu-vertical-demo"
        >
          <div style="color:cornflowerblue;text-align:center;margin: 13px;font-size: 16px" >
            <img src="../assets/logo.png" style="width: 22px;position: relative;top:5.5px;">
            <span v-show="wzht"><b>&nbsp;红太阳后台管理</b></span>
          </div>
          <el-submenu index="1">
            <template slot="title"><i class="el-icon-message"></i><span slot="title">销售管理</span></template>
              <el-menu-item index="1-1">产品价格</el-menu-item>
              <el-menu-item index="1-2">销售下单</el-menu-item>
               <el-menu-item index="1-3">销售薪资</el-menu-item>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title"><i class="el-icon-menu"></i><span slot="title">生产管理</span></template>
              <el-menu-item index="2-1">产品管理</el-menu-item>
              <el-menu-item index="2-2">生产绩效</el-menu-item>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title"><i class="el-icon-setting"></i><span slot="title">推广管理</span></template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="3-1">选项1</el-menu-item>
              <el-menu-item index="3-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="3-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="3-4">
              <template slot="title">选项4</template>
              <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-container>
        <el-header style="font-size: 16px;border-bottom: 1px solid #ccc">
          <div style="flex:1;font-size:18px">
            <span><i :class="btnClass" style="cursor: pointer" @click="collapse"></i>&nbsp;</span>
          </div>
          <div style="flex:1;font-size: 18px;float: right;position: relative;top:-60px">
          <el-dropdown>
            <span class="el-dropdown-link">谢忠原
                     <i class="el-icon-arrow-down el-icon--right"></i>
            </span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人信息</el-dropdown-item>
              <el-dropdown-item>退出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
          </div>
        </el-header>
        <el-main>
          <el-breadcrumb separator="/">
            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item><a href="/">销售管理</a></el-breadcrumb-item>
            <el-breadcrumb-item>生产管理</el-breadcrumb-item>
            <el-breadcrumb-item>推广管理</el-breadcrumb-item>
          </el-breadcrumb>
          <div class="ml-10">
            <el-input suffix-icon="el-icon-user-solid" v-model="inputName" style="width:180px;margin-right: 10px" type="text" size="medium"  placeholder="请输入姓名" ></el-input>
            <el-input suffix-icon="el-icon-document" v-model="inputDingDan" style="width:180px;margin-right: 10px" type="text" size="medium"  placeholder="请输入订单编号" ></el-input>
            <el-input suffix-icon="el-icon-s-home" v-model="inputFirm" style="width:180px;margin-right: 10px" type="text" size="medium"  placeholder="请输入公司名称" ></el-input>
            <el-button type="primary" style="margin: 10px 5px" icon="el-icon-search" size="medium">搜索</el-button>
          </div>
          <div class="ml-10">
            <el-row>
              <el-button type="success" size="medium" style="width: 90px">增加<i class="el-icon-circle-plus-outline el-icon--right"></i></el-button>
              <el-button type="danger" size="medium" style="width: 90px">删除<i class="el-icon-remove-outline
 el-icon--right"></i></el-button>
              <el-button type="primary" size="medium" style="width: 90px">导入<i class="el-icon-folder-add
 el-icon--right"></i></el-button>
              <el-button type="primary" size="medium" style="width: 90px">导出<i class="el-icon-upload el-icon--right"></i></el-button>
            </el-row>
          </div>
          <el-table :data="tableData" border style="text-align: center">
            <el-table-column
                type="selection"
                width="55">
            </el-table-column>
            <el-table-column prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
            <el-table-column  label="编辑" width="300" fixed="right">
              <template slot-scope="scope">
                <el-button type="primary" size="small" @click="handleClick(scope.row)" >编辑<i class="el-icon-edit el-icon--right"></i></el-button>
                <el-button type="danger" size="small">删除<i class="el-icon-delete el-icon--right"></i></el-button>
              </template>
            </el-table-column>
          </el-table>
          <div class="block" style="padding:10px 0px">
            <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[100, 200, 300, 400]"
                :page-size="100"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
            </el-pagination>
          </div>
        </el-main>
      </el-container>
    </el-container>
</template>

<script>
export default {
  name:'home',
  methods: {
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
    },
    collapse(){
      this.isCollapse=!this.isCollapse
      if(this.isCollapse){
        this.btnClass='el-icon-s-unfold';
        this.dtwidth=64;
        this.wzht=false;
      }else{
        this.btnClass='el-icon-s-fold';
        this.dtwidth=200;
        this.wzht=true;
      }
    }

  },
  data(){
    const item = {
      date: '2016-05-02',
      name: '谢中原',
      address: '奥奇丽工业园区27号楼'
    };
    return {
      currentPage1: 5,
      currentPage2: 5,
      currentPage3: 5,
      currentPage4: 4,
      inputName:'',
      inputDingDan:'',
      inputFirm:'',
      tableData: Array(9).fill(item),
      isCollapse:false,
      dtwidth:200,
      btnClass:'el-icon-s-fold',
      wzht:true,
    };
  }
}
</script>

<style>
.el-header {
  background-color: #B3C0D1;
  color: #333;
  line-height: 60px;
}
.el-aside {
  color: #333;
}
</style>
