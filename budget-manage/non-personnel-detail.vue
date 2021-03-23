<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage/non-personnel-funds">公用经费明细表(行政、事业)</BreadcrumbItem>
                <BreadcrumbItem>档案详情</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'non-personnel-funds'}"><div class="go-back">返回</div></router-link>
        </div>
        <!--表单信息-->
        <Row class="common">
            <Col class="com-title">
                <div>基本信息</div>
                <!--<div>预算年度:-->
                <!--<Select v-model="postList.moneyState" size="large" style="width:200px;text-align: left">-->
                <!--<Option value="">2019</Option>-->
                <!--<Option value="0">2020</Option>-->
                <!--<Option value="1">2021</Option>-->
                <!--</Select>-->
                <!--</div>-->
            </Col>
            <Col class="com-key" span="5">项目</Col>
            <Col class="com-key" span="5">总计(元)</Col>
            <Col class="com-key" span="4">财政补助收入（元）</Col>
            <Col class="com-key" span="5">其他收入(元)</Col>
            <Col class="com-key" span="5">操作</Col>
            <Col class="com-value" span="5">办公费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.office.total"></InputNumber>-->
                <span>{{postList.office.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.office.financialAid"></InputNumber>-->
                <span>{{postList.office.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.office.otherAid"></InputNumber>-->
                <span>{{postList.office.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('office')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('office')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">印刷费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.printingExpenses.total"></InputNumber>-->
                <span>{{postList.printingExpenses.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.printingExpenses.financialAid"></InputNumber>-->
                <span>{{postList.printingExpenses.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.printingExpenses.otherAid"></InputNumber>-->
                <span>{{postList.printingExpenses.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('printingExpenses')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('printingExpenses')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">咨询费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.consultingFee.total"></InputNumber>-->
                <span>{{postList.consultingFee.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.consultingFee.financialAid"></InputNumber>-->
                <span>{{postList.consultingFee.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.consultingFee.otherAid"></InputNumber>-->
                <span>{{postList.consultingFee.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('consultingFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('consultingFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">手续费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.poundage.total"></InputNumber>-->
                <span>{{postList.poundage.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.poundage.financialAid"></InputNumber>-->
                <span>{{postList.poundage.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.poundage.otherAid"></InputNumber>-->
                <span>{{postList.poundage.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('poundage')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('poundage')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">水费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.water.total"></InputNumber>-->
                <span>{{postList.water.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.water.financialAid"></InputNumber>-->
                <span>{{postList.water.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.water.otherAid"></InputNumber>-->
                <span>{{postList.water.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('water')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('water')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">电费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.electricity.total"></InputNumber>-->
                <span>{{postList.electricity.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.electricity.financialAid"></InputNumber>-->
                <span>{{postList.electricity.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.electricity.otherAid"></InputNumber>-->
                <span>{{postList.electricity.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('electricity')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('electricity')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">邮电费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.postFee.total"></InputNumber>-->
                <span>{{postList.postFee.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.postFee.financialAid"></InputNumber>-->
                <span>{{postList.postFee.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.postFee.otherAid"></InputNumber>-->
                <span>{{postList.postFee.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('postFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('postFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">差旅费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.travel.total"></InputNumber>-->
                <span>{{postList.travel.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.travel.financialAid"></InputNumber>-->
                <span>{{postList.travel.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.travel.otherAid"></InputNumber>-->
                <span>{{postList.travel.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('travel')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('travel')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">因公出国(境)费用</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.abroadOnBusiness.total"></InputNumber>-->
                <span>{{postList.abroadOnBusiness.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.abroadOnBusiness.financialAid"></InputNumber>-->
                <span>{{postList.abroadOnBusiness.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.abroadOnBusiness.otherAid"></InputNumber>-->
                <span>{{postList.abroadOnBusiness.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('abroadOnBusiness')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('abroadOnBusiness')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">日常维修(护)费用</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.dailyMaintenanceFee.total"></InputNumber>-->
                <span>{{postList.dailyMaintenanceFee.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.dailyMaintenanceFee.financialAid"></InputNumber>-->
                <span>{{postList.dailyMaintenanceFee.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.dailyMaintenanceFee.otherAid"></InputNumber>-->
                <span>{{postList.dailyMaintenanceFee.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('dailyMaintenanceFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('dailyMaintenanceFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">租赁费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.rent.total"></InputNumber>-->
                <span>{{postList.rent.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.rent.financialAid"></InputNumber>-->
                <span>{{postList.rent.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.rent.otherAid"></InputNumber>-->
                <span>{{postList.rent.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('rent')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('rent')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">物业管理费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.propertyManagementFee.total"></InputNumber>-->
                <span>{{postList.propertyManagementFee.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.propertyManagementFee.financialAid"></InputNumber>-->
                <span>{{postList.propertyManagementFee.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.propertyManagementFee.otherAid"></InputNumber>-->
                <span>{{postList.propertyManagementFee.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('propertyManagementFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('propertyManagementFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">会议费(三类会议)</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.conferenceExpenseThree.total"></InputNumber>-->
                <span>{{postList.conferenceExpenseThree.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.conferenceExpenseThree.financialAid"></InputNumber>-->
                <span>{{postList.conferenceExpenseThree.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.conferenceExpenseThree.otherAid"></InputNumber>-->
                <span>{{postList.conferenceExpenseThree.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('conferenceExpenseThree')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('conferenceExpenseThree')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">会议费(四类会议)</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.conferenceExpenseFour.total"></InputNumber>-->
                <span>{{postList.conferenceExpenseFour.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.conferenceExpenseFour.financialAid"></InputNumber>-->
                <span>{{postList.conferenceExpenseFour.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.conferenceExpenseFour.otherAid"></InputNumber>-->
                <span>{{postList.conferenceExpenseFour.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('conferenceExpenseFour')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('conferenceExpenseFour')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">培训费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.training.total"></InputNumber>-->
                <span>{{postList.training.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.training.financialAid"></InputNumber>-->
                <span>{{postList.training.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.training.otherAid"></InputNumber>-->
                <span>{{postList.training.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('training')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('training')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">公务接待费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officialReceptionFee.total"></InputNumber>-->
                <span>{{postList.officialReceptionFee.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officialReceptionFee.financialAid"></InputNumber>-->
                <span>{{postList.officialReceptionFee.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officialReceptionFee.otherAid"></InputNumber>-->
                <span>{{postList.officialReceptionFee.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('officialReceptionFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('officialReceptionFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">专用材料费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.specialCostOfMaterials.total"></InputNumber>-->
                <span>{{postList.specialCostOfMaterials.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.specialCostOfMaterials.financialAid"></InputNumber>-->
                <span>{{postList.specialCostOfMaterials.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.specialCostOfMaterials.otherAid"></InputNumber>-->
                <span>{{postList.specialCostOfMaterials.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('specialCostOfMaterials')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('specialCostOfMaterials')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">被装购置费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.purchaseCostOfThePackage.total"></InputNumber>-->
                <span>{{postList.purchaseCostOfThePackage.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.purchaseCostOfThePackage.financialAid"></InputNumber>-->
                <span>{{postList.purchaseCostOfThePackage.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.purchaseCostOfThePackage.otherAid"></InputNumber>-->
                <span>{{postList.purchaseCostOfThePackage.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('purchaseCostOfThePackage')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('purchaseCostOfThePackage')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">办公设备购置费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officeEquipmentPurchaseCost.total"></InputNumber>-->
                <span>{{postList.officeEquipmentPurchaseCost.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officeEquipmentPurchaseCost.financialAid"></InputNumber>-->
                <span>{{postList.officeEquipmentPurchaseCost.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officeEquipmentPurchaseCost.otherAid"></InputNumber>-->
                <span>{{postList.officeEquipmentPurchaseCost.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('officeEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('officeEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">专用设备购置费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.specialEquipmentPurchaseCost.total"></InputNumber>-->
                <span>{{postList.specialEquipmentPurchaseCost.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.specialEquipmentPurchaseCost.financialAid"></InputNumber>-->
                <span>{{postList.specialEquipmentPurchaseCost.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.specialEquipmentPurchaseCost.otherAid"></InputNumber>-->
                <span>{{postList.specialEquipmentPurchaseCost.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('specialEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('specialEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">其他资本性支出</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.otherCapitalExpenditures.total"></InputNumber>-->
                <span>{{postList.otherCapitalExpenditures.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.otherCapitalExpenditures.financialAid"></InputNumber>-->
                <span>{{postList.otherCapitalExpenditures.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.otherCapitalExpenditures.otherAid"></InputNumber>-->
                <span>{{postList.otherCapitalExpenditures.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('otherCapitalExpenditures')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('otherCapitalExpenditures')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">其他资本性支出 ——图书资料购置费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.otherCapitalExpendituresBook.total"></InputNumber>-->
                <span>{{postList.otherCapitalExpendituresBook.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.otherCapitalExpendituresBook.financialAid"></InputNumber>-->
                <span>{{postList.otherCapitalExpendituresBook.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.otherCapitalExpendituresBook.otherAid"></InputNumber>-->
                <span>{{postList.otherCapitalExpendituresBook.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('otherCapitalExpendituresBook')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('otherCapitalExpendituresBook')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">专用燃料费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.dedicatedFuelCharge.total"></InputNumber>-->
                <span>{{postList.dedicatedFuelCharge.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.dedicatedFuelCharge.financialAid"></InputNumber>-->
                <span>{{postList.dedicatedFuelCharge.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.dedicatedFuelCharge.otherAid"></InputNumber>-->
                <span>{{postList.dedicatedFuelCharge.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('dedicatedFuelCharge')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('dedicatedFuelCharge')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5"> 劳务费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.labor.total"></InputNumber>-->
                <span>{{postList.labor.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.labor.financialAid"></InputNumber>-->
                <span>{{postList.labor.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.labor.otherAid"></InputNumber>-->
                <span>{{postList.labor.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('labor')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('labor')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5"> 委托业务费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.commissionCharge.total"></InputNumber>-->
                <span>{{postList.commissionCharge.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.commissionCharge.financialAid"></InputNumber>-->
                <span>{{postList.commissionCharge.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.commissionCharge.otherAid"></InputNumber>-->
                <span>{{postList.commissionCharge.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('commissionCharge')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('commissionCharge')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">其他商品和服务支出</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.goodsAndServices.total"></InputNumber>-->
                <span>{{postList.goodsAndServices.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.goodsAndServices.financialAid"></InputNumber>-->
                <span>{{postList.goodsAndServices.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.goodsAndServices.otherAid"></InputNumber>-->
                <span>{{postList.goodsAndServices.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('goodsAndServices')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('goodsAndServices')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-total" span="5">小计</Col>
            <Col class="com-total" span="5">
                {{postList.subtotal.totalValue}}
            </Col>
            <Col class="com-total" span="4">
                {{postList.subtotal.financialAidValue}}
            </Col>
            <Col class="com-total" span="5">
                {{postList.subtotal.otherAidValue}}
            </Col>
            <Col class="com-total" span="5">
                <span>/</span>
            </Col>
            <Col class="com-value" span="5"> 工会经费（2%）</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.unionFunds.total"></InputNumber>-->
                <span>{{postList.unionFunds.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.unionFunds.financialAid"></InputNumber>-->
                <span>{{postList.unionFunds.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.unionFunds.otherAid"></InputNumber>-->
                <span>{{postList.unionFunds.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('unionFunds')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('unionFunds')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">福利费（360元/人）</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.welfareFunds.total"></InputNumber>-->
                <span>{{postList.welfareFunds.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.welfareFunds.financialAid"></InputNumber>-->
                <span>{{postList.welfareFunds.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.welfareFunds.otherAid"></InputNumber>-->
                <span>{{postList.welfareFunds.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('welfareFunds')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('welfareFunds')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">办公用房物业管理费</Col>
            <Col class="com-value" span="5">
                <span>{{postList.officePremises.totalValue}}</span>
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officePremises.total"></InputNumber>-->
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.officePremises.financialAidValue}}</span>
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officePremises.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="5">
                <span>{{postList.officePremises.otherAidValue}}</span>
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officePremises.otherAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('officePremises')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('officePremises')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">交通工具运行维护费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFee.total"></InputNumber>-->
                <span>{{postList.maintenanceFee.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFee.financialAid"></InputNumber>-->
                <span>{{postList.maintenanceFee.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFee.otherAid"></InputNumber>-->
                <span>{{postList.maintenanceFee.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('maintenanceFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('maintenanceFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5" style="text-align: right">其中:公务用车运行维护费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeBus.total"></InputNumber>-->
                <span>{{postList.maintenanceFeeBus.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeBus.financialAid"></InputNumber>-->
                <span>{{postList.maintenanceFeeBus.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeBus.otherAid"></InputNumber>-->
                <span>{{postList.maintenanceFeeBus.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('maintenanceFeeBus')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('maintenanceFeeBus')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5"><span style="position: relative;left: 60px">其中:其他交通费用</span></Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeOther.total"></InputNumber>-->
                <span>{{postList.maintenanceFeeOther.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeOther.financialAid"></InputNumber>-->
                <span>{{postList.maintenanceFeeOther.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeOther.otherAid"></InputNumber>-->
                <span>{{postList.maintenanceFeeOther.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('maintenanceFeeOther')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('maintenanceFeeOther')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-total" span="5">小计</Col>
            <Col class="com-total" span="5">
                {{postList.subtotalTwo.totalValue}}
            </Col>
            <Col class="com-total" span="4">
                {{postList.subtotalTwo.financialAidValue}}
            </Col>
            <Col class="com-total" span="5">
                {{postList.subtotalTwo.otherAidValue}}
            </Col>
            <Col class="com-total" span="5">
                <span>/</span>
            </Col>
            <Col class="com-value" span="5">办公用房租赁费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officeRent.total"></InputNumber>-->
                <span>{{postList.officeRent.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.officeRent.financialAidValue}}</span>
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officeRent.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="5">
                <span>{{postList.officeRent.otherAidValue}}</span>
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.officeRent.otherAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('officeRent')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <span @click="getDetails('officeRent')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-total"  span="5" >公用经费合计</Col>
            <Col class="com-total" span="5">
                {{postList.totalPublicFunds.totalValue}}
            </Col>
            <Col class="com-total" span="4">
                {{postList.totalPublicFunds.financialAidValue}}
            </Col>
            <Col class="com-total" span="5">
                {{postList.totalPublicFunds.otherAidValue}}
            </Col>
            <Col class="com-total" span="5">
                <span>/</span>
            </Col>
        </Row>
        <!--提交-->
        <!--<Button @click="sureSubmit" class="sure-btn" type="primary">确认</Button>-->
        <Drawer v-model="drawer"
                width=95%
                @on-close="drawerCancel"
                :mask-closable="false"
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col span="24" class="com-title">公用经费合计明细<span class="add-detail" @click="addItem">新增明细</span></Col>
                <Col span="2" class="com-key">明细内容</Col>
                <Col span="1" class="com-key">规格</Col>
                <Col span="1" class="com-key">数量</Col>
                <Col span="1" class="com-key">单价(元)</Col>
                <Col span="2" class="com-key">明细金额(元)</Col>
                <Col span="2" class="com-key">拨付方式</Col>
                <Col span="2" class="com-key">中小企业预留</Col>
                <Col span="2" class="com-key">采购品目</Col>
                <Col span="2" class="com-key">政府采购形式</Col>
                <Col span="1" class="com-key">采购目录</Col>
                <Col span="1" class="com-key">采购方式</Col>
                <Col span="1" class="com-key">是否自主创新</Col>
                <Col span="1" class="com-key">财政补助收入(元)</Col>
                <Col span="2" class="com-key">其他收入(元)</Col>
                <Col span="1" class="com-key">总计(元)</Col>
                <Col span="2" class="com-key">备注</Col>
                <div v-for="(item,index) in  postList[listPre]">
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.compositionDetails" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <Input type="text" v-model="item.specifications" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <Input type="text" v-model="item.price" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <Input type="text" v-model="item.number" class="value-input"></Input>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.detailPrice" class="value-input"></Input>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.projectGrant" class="value-input"></Input>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.unitReserve" class="value-input"></Input>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.purchaseItem" class="value-input"></Input>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.governmentPurchaseMethod" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <Input type="text" v-model="item.purchaseContents" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <Input type="text" v-model="item.purchaseMethod" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <Input type="text" v-model="item.wasIndependentInnovation" class="value-input"></Input>
                    </Col>
                    <Col span="1" class="com-value">
                        <InputNumber :min="0" v-model="item.financialAid" class="value-input"></InputNumber>
                    </Col>
                    <Col span="2" class="com-value">
                        <InputNumber :min="0" v-model="item.otherAid" class="value-input"></InputNumber>
                    </Col>
                    <Col span="1" class="com-value">
                        <InputNumber :min="0"  v-model="item.total" class="value-input"></InputNumber>
                    </Col>
                    <Col span="2" class="com-value">
                        <Input type="text" v-model="item.remarks" class="value-input"></Input>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">
                    </Col>
                </div>

            </Row>
            <div  class="d-footer">
                <Button type="default" @click="drawerCancel">取消</Button>
                <Button type="primary" @click="drawerSave">保存</Button>
            </div>
        </Drawer>
        <Drawer v-model="viewDrawer"
                width=95%
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col span="24" class="com-title">公用经费合计明细</Col>
                <Col span="1" class="com-key">明细内容</Col>
                <Col span="1" class="com-key">规格</Col>
                <Col span="1" class="com-key">数量</Col>
                <Col span="1" class="com-key">单价(元)</Col>
                <Col span="2" class="com-key">明细金额(元)</Col>
                <Col span="2" class="com-key">拨付方式</Col>
                <Col span="2" class="com-key">中小企业预留</Col>
                <Col span="2" class="com-key">采购品目</Col>
                <Col span="2" class="com-key">政府采购形式</Col>
                <Col span="1" class="com-key">采购目录</Col>
                <Col span="1" class="com-key">采购方式</Col>
                <Col span="1" class="com-key">是否自主创新</Col>
                <Col span="2" class="com-key">财政补助收入(元)</Col>
                <Col span="2" class="com-key">其他收入(元)</Col>
                <Col span="1" class="com-key">总计(元)</Col>
                <Col span="2" class="com-key">备注</Col>
                <div v-for="(item,index) in  postList[listPre]">
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.compositionDetails">{{item.compositionDetails}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.specifications">{{item.specifications}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.price">{{item.priceValue}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.number">{{item.numberValue}}</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.detailPrice">{{item.detailPriceValue}}</span>

                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.projectGrant">{{item.projectGrant}}</span>

                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.unitReserve">{{item.unitReserve}}</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.purchaseItem">{{item.purchaseItem}}</span>

                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.governmentPurchaseMethod">{{item.governmentPurchaseMethod}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.purchaseContents">{{item.purchaseContents}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.purchaseMethod">{{item.purchaseMethod}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span v-if="item.wasIndependentInnovation==0">否</span>
                        <span v-if="item.wasIndependentInnovation==1">是</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.financialAid">{{item.financialAidValue}}</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.otherAid">{{item.otherAidValue}}</span>

                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.total">{{item.totalValue}}</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.remarks">{{item.remarks}}</span>
                    </Col>
                </div>

            </Row>
            <!--<div  class="d-footer">-->
            <!--<Button type="default" @click="drawerCancel">取消</Button>-->
            <!--<Button type="primary" @click="drawer = false">保存</Button>-->
            <!--</div>-->
        </Drawer>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        drawer:false,
        viewDrawer:false,
        styles: {
          height: 'calc(100% - 55px)',
          overflow: 'auto',
          paddingBottom: '53px',
          position: 'static'
        },
        listPre:'',
        list:'',
        postList:{
          publicId:this.$route.query.id,
          office:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          printingExpenses:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          printingExpensesDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          consultingFee:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          consultingFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          poundage:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          poundageDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          water:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          waterDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          electricity:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          electricityDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          postFee:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          postFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          travel:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          travelDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          abroadOnBusiness:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          abroadOnBusinessDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          dailyMaintenanceFee:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          dailyMaintenanceFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          rent:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          rentDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          propertyManagementFee:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          propertyManagementFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          conferenceExpenseThree:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          conferenceExpenseThreeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          conferenceExpenseFour:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          conferenceExpenseFourDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          training:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          trainingDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          officialReceptionFee:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officialReceptionFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          specialCostOfMaterials:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          specialCostOfMaterialsDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          purchaseCostOfThePackage:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          purchaseCostOfThePackageDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          officeEquipmentPurchaseCost:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officeEquipmentPurchaseCostDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          specialEquipmentPurchaseCost:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          specialEquipmentPurchaseCostDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          otherCapitalExpenditures:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          otherCapitalExpendituresDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          otherCapitalExpendituresBook:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          otherCapitalExpendituresBookDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          dedicatedFuelCharge:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          dedicatedFuelChargeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          labor:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          laborDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          commissionCharge:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          commissionChargeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          goodsAndServices:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          goodsAndServicesDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          subtotal:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          unionFunds:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          unionFundsDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          welfareFunds:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          welfareFundsDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          officePremises:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officePremisesDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          maintenanceFee:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          maintenanceFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          maintenanceFeeBus:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          maintenanceFeeBusDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          maintenanceFeeOther:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          maintenanceFeeOtherDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          subtotalTwo:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officeRent:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officeRentDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": 0,//单价
              "number":0 ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": '',//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          totalPublicFunds:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
        },
      }
    },
    mounted(){
      this.initList()
    },
    methods: {
      initList(){
        this.$http.get('/api/budgetManage/queryBudgetFundsPublicProject?publicId='+this.$route.query.id).then(res=>{
          this.postList =  res.result.budgetFundsPublicDetail;
        })
      },
      editDetails(item){
        this.drawer = true;
        let temp = item + 'DetailList';
        let temp2 = item;
        this.listPre = temp;
        this.list = temp2;
      },
      getDetails(item){
        this.viewDrawer = true;
        item += 'DetailList';
        this.listPre = item;
      },
      addItem(){
        let obj = {};
        obj.compositionDetails = '';
        obj.specifications = '';
        obj.price = '';
        obj.number = '';
        obj.detailPrice = '';
        obj.projectGrant = '';
        obj.unitReserve = '';
        obj.governmentPurchaseMethod = '';
        obj.purchaseContents = '';
        obj.purchaseItem = '';
        obj.purchaseMethod = '';
        obj.wasIndependentInnovation = '';
        obj.total = '';
        obj.financialAid = '';
        obj.otherAid = '';
        obj.remarks = '';
        this.postList[this.listPre].push(obj)
      },
      deleteDetailItem(index){
        if(this.postList[this.listPre].length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList[this.listPre].splice(index,1)
        }
      },
      drawerCancel(){
        this.postList[this.listPre] = [];
        let obj = {};
        obj.compositionDetails = '';
        obj.specifications = '';
        obj.price = '';
        obj.number = '';
        obj.detailPrice = '';
        obj.projectGrant = '';
        obj.unitReserve = '';
        obj.governmentPurchaseMethod = '';
        obj.purchaseContents = '';
        obj.purchaseItem = '';
        obj.purchaseMethod = '';
        obj.wasIndependentInnovation = '';
        obj.total = '';
        obj.financialAid = '';
        obj.otherAid = '';
        obj.remarks = '';
        this.postList[this.listPre].push(obj)
      },
      drawerSave(){
        this.drawer = false;
        this.postList[this.list].total = this.postList[this.list].financialAid = this.postList[this.list].otherAid = 0;
        this.postList[this.listPre].forEach(item=>{
          this.postList[this.list].total += item.total;
          this.postList[this.list].financialAid += item.financialAid;
          this.postList[this.list].otherAid += item.otherAid;
        });
        this.postList.subtotal.total = this.postList.office.total + this.postList.printingExpenses.total + this.postList.consultingFee.total + this.postList.poundage.total +
          this.postList.water.total + this.postList.electricity.total + this.postList.postFee.total + this.postList.travel.total + this.postList.abroadOnBusiness.total +
          this.postList.dailyMaintenanceFee.total + this.postList.rent.total + this.postList.propertyManagementFee.total + this.postList.conferenceExpenseThree.total +
          this.postList.conferenceExpenseFour.total +this.postList.training.total + this.postList.officialReceptionFee.total + this.postList.specialCostOfMaterials.total +
          this.postList.purchaseCostOfThePackage.total + this.postList.officeEquipmentPurchaseCost.total + this.postList.specialEquipmentPurchaseCost.total +
          this.postList.otherCapitalExpenditures.total + this.postList.otherCapitalExpendituresBook.total + this.postList.dedicatedFuelCharge.total +
          this.postList.labor.total + this.postList.commissionCharge.total + this.postList.goodsAndServices.total;
        this.postList.subtotal.financialAid = this.postList.office.financialAid + this.postList.printingExpenses.financialAid + this.postList.consultingFee.financialAid + this.postList.poundage.financialAid +
          this.postList.water.financialAid + this.postList.electricity.financialAid + this.postList.postFee.financialAid + this.postList.travel.financialAid + this.postList.abroadOnBusiness.financialAid +
          this.postList.dailyMaintenanceFee.financialAid + this.postList.rent.financialAid + this.postList.propertyManagementFee.financialAid + this.postList.conferenceExpenseThree.financialAid +
          this.postList.conferenceExpenseFour.financialAid +this.postList.training.financialAid + this.postList.officialReceptionFee.financialAid + this.postList.specialCostOfMaterials.financialAid +
          this.postList.purchaseCostOfThePackage.financialAid + this.postList.officeEquipmentPurchaseCost.financialAid + this.postList.specialEquipmentPurchaseCost.financialAid +
          this.postList.otherCapitalExpenditures.financialAid + this.postList.otherCapitalExpendituresBook.financialAid + this.postList.dedicatedFuelCharge.financialAid +
          this.postList.labor.financialAid + this.postList.commissionCharge.financialAid + this.postList.goodsAndServices.financialAid;
        this.postList.subtotal.otherAid = this.postList.office.otherAid + this.postList.printingExpenses.otherAid + this.postList.consultingFee.otherAid + this.postList.poundage.otherAid +
          this.postList.water.otherAid + this.postList.electricity.otherAid + this.postList.postFee.otherAid + this.postList.travel.otherAid + this.postList.abroadOnBusiness.otherAid +
          this.postList.dailyMaintenanceFee.otherAid + this.postList.rent.otherAid + this.postList.propertyManagementFee.otherAid + this.postList.conferenceExpenseThree.otherAid +
          this.postList.conferenceExpenseFour.otherAid +this.postList.training.otherAid + this.postList.officialReceptionFee.otherAid + this.postList.specialCostOfMaterials.otherAid +
          this.postList.purchaseCostOfThePackage.otherAid + this.postList.officeEquipmentPurchaseCost.otherAid + this.postList.specialEquipmentPurchaseCost.otherAid +
          this.postList.otherCapitalExpenditures.otherAid + this.postList.otherCapitalExpendituresBook.otherAid + this.postList.dedicatedFuelCharge.otherAid +
          this.postList.labor.otherAid + this.postList.commissionCharge.otherAid + this.postList.goodsAndServices.otherAid;
        this.postList.subtotalTwo.total = this.postList.unionFunds.total + this.postList.welfareFunds.total + this.postList.officePremises.total + this.postList.maintenanceFee.total +
          this.postList.maintenanceFeeBus.total + this.postList.maintenanceFeeOther.total;
        this.postList.subtotalTwo.financialAid = this.postList.unionFunds.financialAid + this.postList.welfareFunds.financialAid + this.postList.officePremises.financialAid + this.postList.maintenanceFee.financialAid +
          this.postList.maintenanceFeeBus.financialAid + this.postList.maintenanceFeeOther.financialAid;
        this.postList.subtotalTwo.otherAid = this.postList.unionFunds.otherAid + this.postList.welfareFunds.otherAid + this.postList.officePremises.otherAid + this.postList.maintenanceFee.otherAid +
          this.postList.maintenanceFeeBus.otherAid + this.postList.maintenanceFeeOther.otherAid;
        this.postList.totalPublicFunds.total = this.postList.subtotal.total + this.postList.subtotalTwo.total + this.postList.officeRent.total;
        this.postList.totalPublicFunds.financialAid = this.postList.subtotal.financialAid + this.postList.subtotalTwo.financialAid + this.postList.officeRent.financialAid;
        this.postList.totalPublicFunds.otherAid = this.postList.subtotal.otherAid + this.postList.subtotalTwo.otherAid + this.postList.officeRent.otherAid;


      },
      sureSubmit(){
        this.$http.post('/api/budgetManage/saveBudgetFundsPublicProject',this.postList).then(res=>{
          this.$Message.success(res.messageContent)
          this.$router.push({name:'non-personnel-funds'})
        })
      },
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
    .add-detail{
        float: right;
        margin-right: 15px;
        cursor: pointer;
        color: #0294e9;
    }
    .add-icon{
        float: right;
        position: relative;
        top: -35px;
        left: 30px;
        cursor: pointer;
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