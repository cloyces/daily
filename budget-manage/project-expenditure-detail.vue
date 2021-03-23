<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage/non-personnel-funds">项目支出预算情况表</BreadcrumbItem>
                <BreadcrumbItem>档案详情</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'project-expenditure'}"><div class="go-back">返回</div></router-link>
        </div>
        <!--表单信息-->
        <Row class="common">
            <Col class="com-title" span="24">
                <span>一级项目</span>
                <div style="float: right">预算年度:
                    <DatePicker type="year"
                                @on-change="postList.firstProject.year = $event"
                                readonly
                                :value="postList.firstProject.year"
                                style="width: 280px">
                    </DatePicker>
                </div>
            </Col>
            <Col class="com-key"  span="4">单位编码</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.unitCode" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">单位名称</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.unitName" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">项目编码</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.projectCode" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">项目名称</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.projectName" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">项目类别</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.projectType" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">项目状态</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.projectStatus" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">是否绩效</Col>
            <Col class="com-value" span="8">
                <!--<RadioGroup  v-model="postList.firstProject.wasAchievements">-->
                    <!--<Radio :label="1">是</Radio>-->
                    <!--<Radio :label="0">否</Radio>-->
                <!--</RadioGroup>-->
                <span v-if="postList.firstProject.wasAchievements==1">是</span>
                <span v-if="postList.firstProject.wasAchievements==0">否</span>
            </Col>
            <Col class="com-key"  span="4">未编报方式</Col>
            <Col class="com-value" span="8">
                <Input type="text" v-model="postList.firstProject.notReportedMode" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key-big"  span="4">未编报说明</Col>
            <Col class="com-value-big" span="20">
                <Input type="textarea" v-model="postList.firstProject.notReportedExplain" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key-big"  span="4">预警说明</Col>
            <Col class="com-value-big" span="20">
                <Input type="textarea" v-model="postList.firstProject.warningExplain" readonly class="value-input"></Input>
            </Col>
            <Col class="com-key"  span="4">本年预算(元)</Col>
            <Col class="com-value" span="20">
                <InputNumber :min="0" v-model="postList.firstProject.yearBudgetValue" readonly class="value-input"></InputNumber>
            </Col>
            <Col class="com-title" span="24">
                二级构成
                <!--<div style="float: right">-->
                    <!--<span style="color: #0294e9;cursor: pointer" @click="addSecondItem">新增</span>-->
                <!--</div>-->
            </Col>
            <Col class="com-key" span="2">序号</Col>
            <Col class="com-key" span="10">构成内容</Col>
            <Col class="com-key" span="3">构成金额(元)</Col>
            <Col class="com-key" span="5">资金来源</Col>
            <Col class="com-key" span="4">操作</Col>
            <div v-for="(item , index) in postList.budgetSecondConstitutes">
                <Col class="com-value" span="2">{{index+1}}</Col>
                <Col class="com-value" span="10">
                    <Input type="text" readonly v-model="item.constituteDetail" class="value-input"></Input>
                </Col>
                <Col class="com-value" span="3">{{item.constituteMoneyValue}}</Col>
                <Col class="com-value" span="5">
                    <Input type="text" readonly v-model="item.moneySource" class="value-input"></Input>
                </Col>
                <Col class="com-value" span="4">
                    <span @click="getThirdDetails(index)" style="cursor: pointer;color: #0294E9">明细</span>
                    <!--<span @click="deleteSecondItem(index)" style="cursor: pointer;color: #0294E9;margin-left: 15px">删除</span>-->
                </Col>
            </div>
        </Row>
        <!--提交-->
        <!--<Button @click="sureSubmit" class="sure-btn" type="primary">确认</Button>-->
        <Drawer v-model="drawer"
                width=95%
                @on-close="drawerSave"
                :mask-closable="false"
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col span="24" class="com-title">三级明细
                    <!--<span class="add-detail" @click="addItem">新增明细</span>-->
                </Col>
                <Col span="2" class="com-key">明细内容</Col>
                <Col span="1" class="com-key">规格</Col>
                <Col span="1" class="com-key">数量</Col>
                <Col span="1" class="com-key">单价(元)</Col>
                <Col span="2" class="com-key">明细金额(元)</Col>
                <Col span="2" class="com-key">拨付方式</Col>
                <Col span="2" class="com-key">中小企业预留</Col>
                <Col span="2" class="com-key">采购品目</Col>
                <Col span="2" class="com-key">政府采购形式</Col>
                <Col span="2" class="com-key">是否自主创新</Col>
                <Col span="2" class="com-key">财政补助收入(元)</Col>
                <Col span="2" class="com-key">其他收入(元)</Col>
                <Col span="1" class="com-key">总计(元)</Col>
                <Col span="2" class="com-key">备注</Col>
                <div v-for="(item,index) in totalList">
                    <Col span="2" class="com-value"><Input type="text" v-model="item.details" readonly class="value-input"></Input></Col>
                    <Col span="1" class="com-value"><Input type="text" v-model="item.specifications" readonly class="value-input"></Input></Col>
                    <Col span="1" class="com-value"><InputNumber :min="0"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.number" readonly  class="value-input" @on-blur="getTotal(index)"></InputNumber></Col>
                    <Col span="1" class="com-value"><InputNumber :min="0"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.price" readonly class="value-input" @on-blur="getTotal(index)"></InputNumber></Col>
                    <Col span="2" class="com-value"><InputNumber :min="0"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.detailPrice" readonly class="value-input"></InputNumber></Col>
                    <Col span="2" class="com-value"><Input type="text" v-model="item.grant" readonly class="value-input"></Input></Col>
                    <Col span="2" class="com-value"><Input type="text" v-model="item.unitReserve" readonly class="value-input"></Input></Col>
                    <Col span="2" class="com-value"><Input type="text" v-model="item.purchaseItem" readonly class="value-input"></Input></Col>
                    <Col span="2" class="com-value"><Input type="text" v-model="item.governmentPurchaseMethod" readonly class="value-input"></Input></Col>
                    <Col span="2" class="com-value">
                        <span v-if="item.wasIndependentInnovation==1">是</span>
                        <span v-if="item.wasIndependentInnovation==0">否</span>
                        <!--<Input type="text" v-model="item.wasIndependentInnovation" readonly class="value-input"></Input>-->
                    </Col>
                    <Col span="2" class="com-value"><InputNumber :min="0"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.financialAid" readonly class="value-input" @on-blur="getCheck(index)"></InputNumber></Col>
                    <Col span="2" class="com-value"><InputNumber :min="0"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.otherAid" readonly class="value-input" @on-blur="getCheck(index)"></InputNumber></Col>
                    <Col span="1" class="com-value">
                        <InputNumber :min="0" v-model="item.total"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     readonly class="value-input"></InputNumber>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.remarks" readonly class="value-input"></Input>
                        <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">-->
                    </Col>
                </div>

            </Row>
            <!--<div  class="d-footer">-->
                <!--<Button type="default" @click="drawerCancel">取消</Button>-->
                <!--<Button type="primary" @click="drawerSave" >保存</Button>-->
            <!--</div>-->
        </Drawer>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        drawer:false,
        styles: {
          height: 'calc(100% - 55px)',
          overflow: 'auto',
          paddingBottom: '53px',
          position: 'static'
        },
        secondItemList:[],
        indexNum:'',
        totalList:[],
        postList:{
          firstProject:{
            year:'',//预算年度
            wasAchievements:1,//是否绩效(0.否，1.是)
            "unitCode": "",//单位编码
            "unitName": "",//单位名字
            "projectCode": "",//项目编码
            "projectName": "",//项目名称
            "projectType": "",//项目类别
            "projectStatus": "",//项目状态
            "budgetLink": "",//预算流转环节
            "notReportedMode": "",//未编报方式
            "notReportedExplain": "",//未编报说明
            "warningExplain": "",//预警说明
            yearBudget:0,
          },
          budgetSecondConstitutes:[
            {
              "constituteDetail": "",//构成明细
              "constituteMoney": 0,//构成金额
              "moneySource": "",//资金来源
              "budgetThirdDetailsList":[
                {
                  "details": "",//明细内容
                  "specifications": "",//规格型号
                  "price": 0,//单价
                  "number": 0,//数量
                  "detailPrice": 0,//明细金额
                  "grant": "",//拨款方式
                  "unitReserve": "",//中小企业预留
                  "purchaseItem": "",//采购品目
                  "governmentPurchaseMethod": '',//政府采购形式(字典)
                  "wasIndependentInnovation": '',//是否自主创新
                  "financialAid": 0,//财政补助收入
                  "otherAid": 0,//其他收入
                  "total": 0//总计
                }
              ],//三级明细
            }
          ],
        },
      }
    },
    mounted(){
      this.initList();
    },
    methods: {
      initList(){
        this.$http.get('/api/budgetManage/queryBudgetProject?projectId='+this.$route.query.id).then(res=>{
          this.postList = res.result.detail;
        })
      },
      sureSubmit(){
        this.$http.post('/api/budgetManage/changeBudgetFirstProject',this.postList).then(res=>{
          if(res.messageCode==10000){
            this.$Message.success(res.messageContent);
            this.$router.push({name:'project-expenditure'})
          }else {
            this.$Message.error(res.messageContent);
          }

        })
      },
      addSecondItem(){
        let obj = {};
        obj.constituteDetail = '';
        obj.constituteMoney = '';
        obj.moneySource = '';
        obj.budgetThirdDetailsList = [];
        this.postList.budgetSecondConstitutes.push(obj);
      },
      getThirdDetails(index){
        this.totalList = this.postList.budgetSecondConstitutes[index].budgetThirdDetailsList;
        this.indexNum = index;
        this.drawer = true;
      },
      deleteSecondItem(index){
        this.$Modal.confirm({
          title: "删除确认",
          content: "确定要删除吗？",
          onOk: () => {
            this.postList.budgetSecondConstitutes.splice(index,1)
          }
        });
      },
      addItem(){
        let obj = {};
        obj.details = '';
        obj.specifications = '';
        obj.price = 0;
        obj.number = 0;
        obj.financialAid = 0;
        obj.otherAid = 0;
        obj.total = 0;
        obj.detailPrice = 0;
        obj.grant = '';
        obj.unitReserve = '';
        obj.purchaseItem = '';
        obj.governmentPurchaseMethod = '';
        obj.wasIndependentInnovation = '';
        this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList.push(obj)
      },
      deleteDetailItem(index){
        if(this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList.splice(index,1)
        }
      },
      getTotal(index){
        this.getCheck(index);
        if(this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].price&&this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].number){
          this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].total = this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].number*this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].price;
        }
      },
      getCheck(index){
        if(this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].financialAid&&this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].otherAid){
          let num = this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].number*this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].price;
          let num2 = this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].financialAid + this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList[index].otherAid;
          if(num!==num2){
            this.$Message.error('数量与单价之积需与财政补助收入与其他收入之和相等',3000)
          }
        }
      },
      drawerCancel(){
        this.totalList = [];
        this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList = [];
        this.addItem();
      },
      drawerSave(){
        this.drawer = false;
        this.postList.budgetSecondConstitutes[this.indexNum].constituteMoney = 0;
        this.postList.budgetSecondConstitutes[this.indexNum].budgetThirdDetailsList.forEach(item=>{
          this.postList.budgetSecondConstitutes[this.indexNum].constituteMoney += item.total;
        });
      }
    }
  }
</script>

<style lang="scss" scoped>
    .common{
        text-align: center;
        border-right: 1px solid #cfcfcf;
        border-bottom: 1px solid #cfcfcf;
        font-family: '思源黑体 CN';
        font-weight: 400;
        margin-right: 15px;
    }
    .com-title{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        background-color: #EEF5FD;
        font-size: 16px;
        div{
            padding-left: 20px;
            margin-right: 20px;
        }

    }
    .com-key{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        background-color: #F6FCFF;
    }
    .com-key-big{
        height: 120px;
        line-height: 120px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        background-color: #F6FCFF;
    }
    .com-total{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        background-color: #F9F9F9;
    }
    .com-value{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        border-right: none;
        background: #FFFFFF;
    }
    .com-value-big{
        height: 120px;
        line-height: 120px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        border-right: none;
        background: #FFFFFF;
    }
    .add-icon{
        float: right;
        position: relative;
        top: -35px;
        left: 30px;
        cursor: pointer;
    }
    .add-detail{
        float: right;
        margin-right: 15px;
        cursor: pointer;
        color: #0294e9;
    }
    .sure-btn {
        width: 120px;
        height: 40px;
        font-size: 16px;
        display: block;
        margin: 40px auto 0 auto;
    }
    .value-input{
        width: 90%;
        text-align: center;
    }
    .value-ellipsis{
        white-space: nowrap;
        text-overflow:ellipsis;
        overflow:hidden;
    }
    .d-footer{
        margin-top: 200px;
        text-align: center;
        button{
            width: 120px;
            margin-left: 10px;
            height: 40px;
            font-size: 16px;
        }
    }

</style>
