<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <Breadcrumb>
            <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
            <BreadcrumbItem>公用经费明细表（行政、事业）</BreadcrumbItem>
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
                <div class="title"><img src="../../assets/non-personnel-funds.png" alt="">公用经费明细表（行政、事业）</div>
                <div class="handle">
                    <span class="handle-item" @click="nonPersonnelAdd">新建档案</span>
                </div>
            </div>
            <Table :columns="tableColumns" :data="tableData" class="m-table" border ref="table">
                <!--<template  slot-scope="{ row,index }" slot="year">-->
                    <!--<InputNumber :min="0" v-model="row.year" style="width: 90%;text-align: center"></InputNumber>-->
                <!--</template>-->
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
        <Modal v-model="nonPersonnelModal" width="420px">
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
  // import { dragTable } from '../../utils/dragTable'
  // import iviewTableDrag from '../../utils/iviewTableDrag'
  import basePage from '../../components/base-page.vue';
  export default {
    name: "",
    components: {
      basePage
    },
    data() {
      return {
        nonPersonnelModal:false,//新增Modal
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
      // this.$nextTick(() => {
      //   setTimeout(() => {
      //     iviewTableDrag();
      //   }, 1500);
      // });
      // let dom = this.$refs.table.$refs.header.getElementsByTagName("th");
      // dragTable(this,dom);
      this.initList();
    },
    methods: {
      initList(){
        this.$http.post('/api/budgetManage/queryBudgetFundsPublicList',this.postList).then(res=>{
          this.tableData = res.result.budgetFundsPublicInfoList.list;
          this.page.total = res.result.budgetFundsPublicInfoList.total;
        })
      },
      nonPersonnelAdd(){
        this.$router.push({name:'non-personnel-add'})
      },
      addConfirm(){
        this.$http.get('/api/budgetManage/saveBudgetFundsPublicInfo?year='+this.budgetYear).then(res=>{
          if(res.messageCode==10000){
            this.$router.push({name:'non-personnel-add',query:{id:res.result.id}})
          }else {
            this.$Message.info(res.messageContent)
          }
        })
      },
      addCancel(){
        this.nonPersonnelModal = false;
      },
      view(row){
        this.$router.push({name:'non-personnel-detail',query:{id:row.publicId}})
      },
      modify(row){
        this.$router.push({name:'non-personnel-modify',query:{id:row.publicId}})
      },
      del(row){
        this.$Modal.confirm({
          title: "删除确认",
          content: "确定要删除吗？",
          onOk: () => {
            this.$http.get("/api/budgetManage/removeBudgetFundsPublic?publicId=" + row.publicId).then(res => {
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