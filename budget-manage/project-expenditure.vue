<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <Breadcrumb>
            <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
            <BreadcrumbItem>项目支出预算情况表</BreadcrumbItem>
        </Breadcrumb>
        <!--查询条件-->
        <Row class="search-option">
            <Col class="search-option-item" span="5"><span>单位编码：</span>
                <Input type="text" v-model="postList.unitCode"  style="width:200px; text-align: left;"></Input>
            </Col>
            <Col class="search-option-item" span="5"><span>项目编码：</span>
                <Input type="text" v-model="postList.projectCode"  style="width:200px; text-align: left;"></Input>
            </Col>
            <Col class="search-option-item" span="5"><span>项目类别：</span>
                <Input type="text" v-model="postList.projectType"  style="width:200px; text-align: left;"></Input>
            </Col>
            <Col class="search-btn" span="4"><Button @click="initList" size="large" type="primary">查询</Button></Col>
        </Row>
        <!--列表-->
        <div class="list">
            <div class="list-header">
                <div class="title"><img src="../../assets/project-expenditure.png" alt="">项目支出预算情况表</div>
                <div class="handle">
                    <router-link :to="{ name: 'project-expenditure-add'}"><span class="handle-item">新建档案</span></router-link>
                </div>
            </div>
            <Table :columns="tableColumns" :data="tableData" class="m-table" border>
                <template slot-scope="{ row,index }" slot="action">
                    <div class="m-operation">
                        <div class="m-btn-item" @click="view(row)">
                            查看
                        </div>
                        <div  class="m-btn-item" @click="modify(row)">
                            修改
                        </div>
                        <div  class="m-btn-item" @click="del(row)">
                            删除
                        </div>
                    </div>
                </template>
            </Table>
            <div class="m-page">
                <base-page :page="page" @onChange="onChange" @onPageSizeChange="onPageSizeChange"></base-page>
            </div>
        </div>
    </div>
</template>

<script>
  import basePage from '../../components/base-page.vue';
  export default {
    name: "",
    components: {
      basePage
    },
    data() {
      return {
        infoList:[],
        postList:{
          unitCode:'',
          projectCode:'',
          projectType:'',
          page: 1,
          pageSize: 10,
        },
        page:{
          total:0,
          pageSize: 10
        },
        tableColumns:[
          {
            title:'序号',
            type:'index',
            align:'center',
            width:100,
          },
          {
            title:'单位编码',
            key:'unitCode',
          },
          {
            title:'单位名称',
            key:'unitName',
          },
          {
            title:'项目编码',
            key:'projectCode',
          },
          {
            title:'项目名称',
            key:'projectName',
          },
          {
            title:'项目类别',
            key:'projectType',
          },
          {
            title:'本年预算',
            key:'yearBudgetValue',
          },
          {
            title:'操作',
            slot:'action',
          }
        ],
        tableData:[],
      }
    },
    mounted(){
      this.initList();
    },
    methods: {
      initList(){
        this.$http.post('/api/budgetManage/queryProjectSpendList',this.postList).then(res=>{
          this.tableData = res.result.budgetProjectInfoList.list;
          this.page.total = res.result.budgetProjectInfoList.total;
        })
      },
      view(row){
        this.$router.push({name:'project-expenditure-detail',query:{id:row.projectId}})
      },
      modify(row){
        this.$router.push({name:'project-expenditure-modify',query:{id:row.projectId}})
      },
      del(row){
        this.$Modal.confirm({
          title: "删除确认",
          content: "确定要删除吗？",
          onOk: () => {
            this.$http.get("/api/budgetManage/removeProjectSpend?projectId="+row.projectId).then(res => {
              this.$Message.success(res.messageContent);
              this.initList();
            });
          }
        });
      },
      /**页码改变
       * method onChange
       * */
      onChange(page) {
        this.postList.page = page;
        this.initList();
      },
      /**page-size改变
       * method onPageSizeChange
       * */
      onPageSizeChange(pageSize) {
        this.postList.pageSize = pageSize;
        this.initList();
      }
    }
  }
</script>

<style scoped>

</style>