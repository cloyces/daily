<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage">非税收入执收及其他收入项目情况表</BreadcrumbItem>
                <BreadcrumbItem>档案详情</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'budget-manage'}"><div class="go-back">返回</div></router-link>
        </div>
        <!--表单信息-->
        <Row class="common">
            <Col class="com-title">
                <div>基本信息</div>
            </Col>
            <Col class="com-title">一、非税收入执收</Col>
            <Col span="16" class="com-key">收入项目</Col>
            <Col span="4" class="com-key">
                收入金额（元）
            </Col>
            <Col span="4" class="com-key">操作
                <!--<img src="../../assets/icon/add-icon.png" @click="addItem" alt="" class="add-icon">-->
            </Col>
            <div v-for="(item,index) in postList.ruleList">
                <Col span="16" class="com-value value-ellipsis">
                    <!--<Input type="text" v-model="item.program" class="value-input"></Input>-->
                    <span :title="item.program">{{item.program}}</span>
                </Col>
                <Col span="4" class="com-value">
                    <!--<InputNumber :min="0" readonly  v-model="item.total" class="value-input"></InputNumber>-->
                    <span>{{item.totalValue}}</span>
                </Col>
                <Col span="4" class="com-value">
                    <!--<span @click="modifyDetails(index)" style="cursor: pointer;color: #0294E9">编辑明细</span>-->
                    <span @click="getDetails(index)" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看明细</span>
                    <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteItem(index)">-->
                </Col>
            </div>
        </Row>
        <Row class="common" style="margin-top: 20px;border-right: none">
            <Col class="com-title" span="24" style="margin-top: 20px;border-right: 1px solid #cfcfcf;">二、教育收费</Col>
            <Col span="16" class="com-key">收入项目</Col>
            <Col span="8" class="common-key">
                收入金额（元）
                <!--<img src="../../assets/icon/add-icon.png" @click="addEducationItem" alt="" class="add-icon">-->
            </Col>
            <div v-for="(item,index) in postList.educationList">
                <Col span="16" class="com-value value-ellipsis">
                    <!--<Input type="text" v-model="item.program" class="value-input"></Input>-->
                    <span :title="item.program">{{item.program}}</span>
                </Col>
                <Col span="8" class="common-value">
                    {{item.totalValue}}
                    <!--<InputNumber :min="0" v-model="item.total" class="value-input"></InputNumber>-->
                    <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteEducationItem(index)">-->
                </Col>
            </div>
            <Col class="com-title" span="24" style="border-right: 1px solid #cfcfcf;">三、事业单位经营收入</Col>
            <Col span="16" class="com-key">收入项目</Col>
            <Col span="8" class="common-key">
                收入金额（元）
                <!--<img src="../../assets/icon/add-icon.png" @click="addUnitItem" alt="" class="add-icon">-->
            </Col>
            <div v-for="(item,index) in postList.businessUnitList">
                <Col span="16" class="com-value value-ellipsis">
                    <span :title="item.program">{{item.program}}</span>
                    <!--<Input type="text" v-model="item.program" class="value-input"></Input>-->
                </Col>
                <Col span="8" class="common-value">
                    {{item.totalValue}}
                    <!--<Input type="text" v-model="item.total" class="value-input"></Input>-->
                    <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteUnitItem(index)">-->
                </Col>
            </div>
            <Col class="com-title" span="24" style="border-right: 1px solid #cfcfcf;">四、事业收入</Col>
            <Col span="16" class="com-key">收入项目</Col>
            <Col span="8" class="common-key">
                收入金额（元）
                <!--<img src="../../assets/icon/add-icon.png" @click="addCauseItem" alt="" class="add-icon">-->
            </Col>
            <div v-for="(item,index) in postList.businessList">
                <Col span="16" class="com-value value-ellipsis">
                    <span :title="item.program">{{item.program}}</span>
                    <!--<Input type="text" v-model="item.program" class="value-input"></Input>-->
                </Col>
                <Col span="8" class="common-value">
                    {{item.totalValue}}
                    <!--<Input type="text" v-model="item.total" class="value-input"></Input>-->
                    <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteCauseItem(index)">-->
                </Col>
            </div>
            <Col class="com-title" span="24" style="border-right: 1px solid #cfcfcf;">五、其他收入</Col>
            <Col span="16" class="com-key">收入项目</Col>
            <Col span="8" class="common-key">
                收入金额（元）
                <!--<img src="../../assets/icon/add-icon.png" @click="addOtherIncomeItem" alt="" class="add-icon">-->
            </Col>
            <div v-for="(item,index) in postList.otherList">
                <Col span="16" class="com-value value-ellipsis">
                    <span :title="item.program">{{item.program}}</span>
                    <!--<Input type="text" v-model="item.program" class="value-input"></Input>-->
                </Col>
                <Col span="8" class="common-value">
                    {{item.totalValue}}
                    <!--<Input type="text" v-model="item.total" class="value-input"></Input>-->
                    <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteOtherIncomeItem(index)">-->
                </Col>
            </div>
        </Row>
        <!--提交-->
        <!--<Button @click="sureSubmit" class="sure-btn" type="primary">确认</Button>-->
        <Drawer v-model="drawer"
                width=75%
                :styles="styles">
            <div slot="header" class="d-header">非税收入执收明细</div>
            <Row class="common" style="margin-right: 40px">
                <Col class="com-title" span="24">非税收入执收</Col>
                <Col class="com-key" span="8">收入类别</Col>
                <Col class="com-key" span="8">收入项目</Col>
                <Col class="com-key" span="8">收入金额（元）</Col>
                <div v-for="(item,index) in postList.ruleList[indexItem].details">
                    <Col class="com-key" span="8">{{item.incomeTypeValue}}</Col>
                    <Col class="com-value value-ellipsis" span="8"><span :title="item.incomeProject">{{item.incomeProject}}</span></Col>
                    <Col class="com-value" span="8">
                        {{item.incomeMoneyValue}}
                        <!--<img src="../../assets/icon/delete-icon.png" @click="deleteDetailItem(index)" alt="" class="delete-icon">-->
                        <!--<img src="../../assets/icon/add-icon.png" @click="addDetailItem(index,item.dataName)" alt="" class="add-icon">-->
                    </Col>
                </div>
            </Row>
            <!--<div  class="d-footer">-->
            <!--<Button type="default" @click="modifyDrawer = false">取消</Button>-->
            <!--<Button type="primary" >保存</Button>-->
            <!--</div>-->
        </Drawer>
        <Drawer v-model="modifyDrawer"
                width=75%
                @on-close="drawerSave"
                :mask-closable="false"
                :styles="styles">
            <div slot="header" class="d-header">非税收入执收明细</div>
            <Row class="common" style="margin-right: 40px">
                <Col class="com-title" span="24">非税收入执收</Col>
                <Col class="com-key" span="8">收入类别</Col>
                <Col class="com-key" span="8">收入项目</Col>
                <Col class="com-key" span="8">收入金额（元）</Col>
                <div v-for="(item,index) in postList.ruleList[indexItem].details">
                    <Col class="com-key" span="8">
                        {{item.incomeTypeValue}}
                    </Col>
                    <Col class="com-value" span="8">
                        <Input type="text" v-model="item.incomeProject" class="value-input"></Input>
                    </Col>
                    <Col class="com-value" span="8">
                        <InputNumber :min="0" v-model="item.incomeMoney" class="value-input"></InputNumber>
                        <img src="../../assets/icon/delete-icon.png" @click="deleteDetailItem(index)" alt="" class="delete-icon">
                        <img src="../../assets/icon/add-icon.png" @click="addDetailItem(index,item.incomeTypeValue,item.incomeType)" alt="" class="add-icon">
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="drawerCancel">取消</Button>
                <Button type="primary" @click="drawerSave" >保存</Button>
            </div>
        </Drawer>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        drawer:false,
        modifyDrawer:false,
        styles: {
          height: 'calc(100% - 55px)',
          overflow: 'auto',
          paddingBottom: '53px',
          position: 'static'
        },
        itemList:[],
        dictList:[],//明细字典列表
        indexItem:0,
        modifyList:[],//取消时对应copy数组
        postList:{
          ruleList:[
            {program:'',total:0,details:[{
                "incomeType": 200001,
                "incomeTypeValue": "政府性基金收入",
                "incomeProject": "cs",//收入项目
                "incomeMoney": 2.00 //收入项目
              }]},
          ],
          educationList:[
            {program:'',total:0},
          ],
          businessUnitList:[
            {program:'',total:0},
          ],
          businessList:[
            {program:'',total:0},
          ],
          otherList:[
            {program:'',total:0},
          ]
        },
      }
    },
    mounted(){
      this.initList()
    },
    methods: {
      initList(){
        this.$http.get('/api/budgetManage/queryBudgetIncomeInfoContents?incomeId='+this.$route.query.id).then(res=>{
          this.postList = res.result.biDetail;
        })
      },
      getDictData(index){
        this.$http.get('/api/dictionaryData/getDictionaryData?dictId=200000').then(res=>{
          if(this.postList.ruleList[index].total==0){
            let list = res.result.otherProgramBaseInfoDto;
            list.forEach(item=>{
              item.incomeTypeValue = item.dataName;
              item.incomeType = item.dataId;
              item.incomeProject = '';
              item.incomeMoney = 0;
            });
            this.postList.ruleList[index].details = list;
          }
        })
      },
      addItem(){
        let obj = {};
        obj.program = '';
        obj.total = '';
        obj.details = [];
        this.postList.ruleList.push(obj)
      },
      deleteItem(index){
        if(this.postList.ruleList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.ruleList.splice(index, 1)
        }
      },
      getDetails(index){
        this.indexItem = index;
        this.drawer = true;
      },
      modifyDetails(index){
        this.getDictData(index);
        this.modifyDrawer = true;
        this.indexItem = index;
        this.modifyList = this.postList.ruleList[this.indexItem].details;
      },
      drawerCancel(){
        this.modifyDrawer = false;
        this.postList.ruleList[this.indexItem].details = this.modifyList;
      },
      drawerSave(){
        this.modifyDrawer =false;
        let total = 0;
        this.postList.ruleList[this.indexItem].details.forEach(item=>{
          total +=item.incomeMoney;
        });
        this.postList.ruleList[this.indexItem].total = total;
      },
      addDetailItem(index,name,type){
        let obj = {};
        obj.incomeProject = '';
        obj.incomeMoney = 0;
        obj.incomeTypeValue = name;
        obj.incomeType = type;
        this.postList.ruleList[this.indexItem].details.splice(index+1,0,obj)
      },
      deleteDetailItem(index){
        this.$Modal.confirm({
          title: "删除确认",
          content: "确定要删除吗？",
          onOk: () => {
            this.postList.ruleList[this.indexItem].details.splice(index,1)
          }
        })
      },
      addEducationItem(){
        let obj = {};
        obj.program = '';
        obj.money = '';
        this.postList.educationList.push(obj)
      },
      deleteEducationItem(index){
        if(this.postList.educationList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.educationList.splice(index,1)
        }
      },
      addUnitItem(){
        let obj = {};
        obj.program = '';
        obj.money = '';
        this.postList.businessUnitList.push(obj)
      },
      deleteUnitItem(index){
        if(this.postList.businessUnitList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.businessUnitList.splice(index, 1)
        }
      },
      addCauseItem(){
        let obj = {};
        obj.program = '';
        obj.money = '';
        this.postList.businessList.push(obj)
      },
      deleteCauseItem(index){
        if(this.postList.businessList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.businessList.splice(index, 1)
        }
      },
      addOtherItem(){
        let obj = {};
        obj.program = '';
        obj.money = '';
        this.postList.otherList.push(obj)
      },
      deleteOtherItem(index){
        if(this.postList.otherList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.otherList.splice(index, 1)
        }
      },
      addOtherIncomeItem(){
        let obj = {};
        obj.program = '';
        obj.money = '';
        this.postList.otherList.push(obj)
      },
      deleteOtherIncomeItem(index){
        if(this.postList.otherList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.otherList.splice(index, 1)
        }
      },
      sureSubmit(){
        this.postList.incomeId = this.$route.query.id;
        this.$http.post('/api/budgetManage/saveBudgetIncomeInfoContents',this.postList).then(res=>{
          if(res.messageCode==10000){
            this.$Message.success(res.messageContent);
            this.$router.push({name:'budget-manage'})
          }else {
            this.$Message.error(res.messageContent)
          }
        })
      },
    }
  }
</script>

<style lang="scss" scoped>
    .top {
        display: flex;
        justify-content: space-between;
        margin-bottom: 10px;
        .crumb-icon {
            position: relative;
            top: 9px;
            margin-left: 7px;
            margin-right: 10px;
        }
        .go-back {
            width: 80px;
            height: 30px;
            line-height: 28px;
            border: 1px solid #ccc;
            text-align: center;
            color: #666;
            border-radius: 20px;
            cursor: pointer;
            margin-top: 10px;
            margin-right: 20px;
        }
    }
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
    .common-key{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        border-right: 1px solid #cfcfcf;
        background-color: #F6FCFF;
    }
    .com-value{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        border-right: none;
        background: #FFFFFF;
    }
    .common-value{
        height: 60px;
        line-height: 60px;
        border-top: 1px solid #cfcfcf;
        border-left: 1px solid #cfcfcf;
        border-right: 1px solid #cfcfcf;
        background: #FFFFFF;
        /*border-right: none;*/
    }
    .value-input{
        width: 90%;
        text-align: center;
    }
    .add-icon{
        float: right;
        position: relative;
        top: 15px;
        left: 45px;
        cursor: pointer;
    }
    .delete-icon{
        float: right;
        position: relative;
        top: 15px;
        left: 50px;
        cursor: pointer;
    }
    .sure-btn {
        width: 120px;
        height: 40px;
        font-size: 16px;
        display: block;
        margin: 40px auto 0 auto;
    }
    .d-footer{
        margin-top: 100px;
        text-align: center;
        button{
            width: 120px;
            margin-left: 10px;
            height: 40px;
            font-size: 16px;
        }
    }

</style>