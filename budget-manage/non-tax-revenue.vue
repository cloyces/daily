<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <Breadcrumb>
            <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
            <BreadcrumbItem>非税收入执收及其他收入项目情况表</BreadcrumbItem>
        </Breadcrumb>
        <!--查询条件-->
        <Row class="search-option">
            <Col  style="line-height: 80px;text-align: right" span="5"><span>预算年度：</span>
                <DatePicker
                        type="year"  @on-change="postList.year = $event"  :value="postList.year" style="width: 220px">
                </DatePicker>
            </Col>
            <Col class="search-btn" span="4"><Button @click="initList" size="large" type="primary">查询</Button></Col>
        </Row>
        <!--列表-->
        <div class="list">
            <div class="list-header">
                <div class="title"><img src="../../assets/budget-manage.png" alt="">非税收入执收及其他收入项目情况表</div>
                <div class="handle">
                    <span @click="nonTaxAdd" class="handle-item">新建档案</span>
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
        <Modal v-model="nonTaxModal" width="420px">
            <div slot="header" class="m-header">新增档案</div>
            <span>预算年度:</span>
            <DatePicker
                type="year"  @on-change="budgetYear = $event"  :value="budgetYear" style="width: 280px"></DatePicker>
            <div slot="footer">
                <Button type="default" @click="addCancel">取消</Button>
                <Button type="primary" @click="addConfirm">确认</Button>
            </div>
        </Modal>
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
        nonTaxModal:false,//新增Modal
        infoList:[],
        budgetYear:'2020',
        postList: {
          year:'',
          page: 1,
          pageSize: 10
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
            title:'预算年度',
            key:'year',
          },
          {
            title:'总计金额(元)',
            key:'totalValue',
          },
          {
            title:'操作',
            slot:'action',
          }
        ],
        tableData:[
          {year:2020,totalMoney:6500},
        ],
      }
    },
    mounted(){
      this.initList();
    },
    methods: {
      nonTaxAdd(){
        this.$router.push({name:'non-tax-add'})
      },
      addConfirm(){
        this.$http.get('/api/budgetManage/saveBudgetIncome?year='+this.budgetYear).then(res=>{
          if(res.messageCode==10000){
            this.$router.push({name:'non-tax-add',query:{id:res.result.id}})
          }else {
            this.$Message.info(res.messageContent)
          }
        })
      },
      addCancel(){
        this.nonTaxModal = false;
      },
      initList(){
        this.$http.post('/api/budgetManage/queryBudgetIncome',this.postList).then(res=>{
          this.tableData = res.result.budgetIncomeInfoList.list;
          this.page.total = res.result.budgetIncomeInfoList.total;
        })
      },
      view(row){
        this.$router.push({name:'non-tax-detail',query:{id:row.incomeId}})
      },
      modify(row){
        this.$router.push({name:'non-tax-modify',query:{id:row.incomeId}})
      },
      del(row){
        this.$Modal.confirm({
          title: "删除确认",
          content: "确定要删除吗？",
          onOk: () => {
            this.$http.get("/api/budgetManage/removeBudgetIncome?incomeId=" + row.incomeId).then(res => {
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