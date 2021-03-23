<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <Breadcrumb>
            <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
            <BreadcrumbItem>人员经费明细表（事业）</BreadcrumbItem>
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
                <div class="title"><img src="../../assets/funds-detail.png" alt="">人员经费明细表（事业）</div>
                <div class="handle">
                    <span class="handle-item" @click="fundsAdd">新建档案</span>
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
        <Modal v-model="fundsModal" width="420px">
            <div slot="header" class="m-header">新增档案</div>
            <span>预算年度:</span>
            <DatePicker
                    type="year"  @on-change="budgetYear = $event"  :value="budgetYear" style="width: 280px">
            </DatePicker>
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
        fundsModal:false,//新增Modal
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
            title:'财政补助收入总计(元)',
            key:'financialAidValue',
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
        this.$http.post('/api/budgetManage/queryBudgetFundsPeopleInfoList',this.postList).then(res=>{
          this.tableData = res.result.budgetFundsPeopleInfoList.list;
          this.page.total = res.result.budgetFundsPeopleInfoList.total;
        })
      },
      fundsAdd(){
        this.$router.push({name:'funds-add'})
      },
      addConfirm(){
        this.$router.push({name:'funds-add',query:{year:this.budgetYear}})
        // this.$http.get('/api/budgetManage/saveBudgetFundsPeople?year='+this.budgetYear).then(res=>{
        //   if(res.messageCode==10000){
        //     this.$router.push({name:'funds-add',query:{year:this.budgetYear}})
        //   }else {
        //     this.$Message.info(res.messageContent)
        //   }
        // })
      },
      addCancel(){
        this.fundsModal = false;
      },
      view(row){
        this.$router.push({name:'funds-view',query:{id:row.peopleId}})
      },
      modify(row){
        this.$router.push({name:'funds-modify',query:{id:row.peopleId}})
      },
      del(row){
        this.$Modal.confirm({
          title: "删除确认",
          content: "确定要删除吗？",
          onOk: () => {
            this.$http.get("/api/budgetManage/removeBudgetFundsPeople?peopleId=" + row.peopleId).then(res => {
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