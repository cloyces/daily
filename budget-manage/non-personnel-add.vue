<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage/non-personnel-funds">公用经费明细表(行政、事业)</BreadcrumbItem>
                <BreadcrumbItem>新建档案</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'non-personnel-funds'}"><div class="go-back">返回</div></router-link>
        </div>
        <!--表单信息-->
        <Row class="common">
            <Col class="com-title" style="display: flex;justify-content: space-between">
                <div>基本信息</div>
                <div>
                    <span class="m-written">*</span>
                    预算年度:
                    <DatePicker
                            type="year"  @on-change="year = $event"  :value="year" style="width: 220px">
                    </DatePicker>
                </div>
            </Col>
            <!--<Col class="com-title">-->
                <!--<div>基本信息</div>-->
                <!--&lt;!&ndash;<div>预算年度:&ndash;&gt;-->
                <!--&lt;!&ndash;<Select v-model="postList.moneyState" size="large" style="width:200px;text-align: left">&ndash;&gt;-->
                <!--&lt;!&ndash;<Option value="">2019</Option>&ndash;&gt;-->
                <!--&lt;!&ndash;<Option value="0">2020</Option>&ndash;&gt;-->
                <!--&lt;!&ndash;<Option value="1">2021</Option>&ndash;&gt;-->
                <!--&lt;!&ndash;</Select>&ndash;&gt;-->
                <!--&lt;!&ndash;</div>&ndash;&gt;-->
            <!--</Col>-->
            <Col class="com-key" span="5">项目</Col>
            <Col class="com-key" span="5">总计(元)</Col>
            <Col class="com-key" span="4">财政补助收入（元）</Col>
            <Col class="com-key" span="5">其他收入(元)</Col>
            <Col class="com-key" span="5">操作</Col>
            <Col class="com-value" span="5">办公费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.office.total"></InputNumber>-->
                <span>{{postList.office.total}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.office.financialAid"></InputNumber>-->
                <span>{{postList.office.financialAid}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.office.otherAid"></InputNumber>-->
                <span>{{postList.office.otherAid}}</span>
            </Col>
            <Col class="com-value" span="5">
                <span @click="editDetails('office')" style="cursor: pointer;color: #0294E9">编辑</span>
                <span @click="getDetails('office')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">印刷费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.printingExpenses.total"></InputNumber>
                <!--<span>{{postList.printingExpenses.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.printingExpenses.financialAid"></InputNumber>
                <!--<span>{{postList.printingExpenses.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange"  v-model="postList.printingExpenses.otherAid"></InputNumber>
                <!--<span>{{postList.printingExpenses.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <!--<span @click="editDetails('printingExpenses')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('printingExpenses')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
                <span>/</span>
            </Col>
            <Col class="com-value" span="5">咨询费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.consultingFee.total"></InputNumber>
                <!--<span>{{postList.consultingFee.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.consultingFee.financialAid"></InputNumber>
                <!--<span>{{postList.consultingFee.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.consultingFee.otherAid"></InputNumber>
                <!--<span>{{postList.consultingFee.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('consultingFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('consultingFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">手续费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"  readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.poundage.total"></InputNumber>
                <!--<span>{{postList.poundage.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.poundage.financialAid"></InputNumber>
                <!--<span>{{postList.poundage.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.poundage.otherAid"></InputNumber>
                <!--<span>{{postList.poundage.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('poundage')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('poundage')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">水费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.water.total"></InputNumber>
                <!--<span>{{postList.water.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.water.financialAid"></InputNumber>
                <!--<span>{{postList.water.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.water.otherAid"></InputNumber>
                <!--<span>{{postList.water.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('water')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('water')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">电费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.electricity.total"></InputNumber>
                <!--<span>{{postList.electricity.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.electricity.financialAid"></InputNumber>
                <!--<span>{{postList.electricity.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.electricity.otherAid"></InputNumber>
                <!--<span>{{postList.electricity.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('electricity')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('electricity')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">邮电费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.postFee.total"></InputNumber>
                <!--<span>{{postList.postFee.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.postFee.financialAid"></InputNumber>
                <!--<span>{{postList.postFee.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.postFee.otherAid"></InputNumber>
                <!--<span>{{postList.postFee.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('postFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('postFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">差旅费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.travel.total"></InputNumber>
                <!--<span>{{postList.travel.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.travel.financialAid"></InputNumber>
                <!--<span>{{postList.travel.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.travel.otherAid"></InputNumber>
                <!--<span>{{postList.travel.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('travel')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('travel')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">因公出国(境)费用</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.abroadOnBusiness.total"></InputNumber>
                <!--<span>{{postList.abroadOnBusiness.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.abroadOnBusiness.financialAid"></InputNumber>
                <!--<span>{{postList.abroadOnBusiness.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.abroadOnBusiness.otherAid"></InputNumber>
                <!--<span>{{postList.abroadOnBusiness.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('abroadOnBusiness')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('abroadOnBusiness')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">日常维修(护)费用</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.dailyMaintenanceFee.total"></InputNumber>
                <!--<span>{{postList.dailyMaintenanceFee.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.dailyMaintenanceFee.financialAid"></InputNumber>
                <!--<span>{{postList.dailyMaintenanceFee.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.dailyMaintenanceFee.otherAid"></InputNumber>
                <!--<span>{{postList.dailyMaintenanceFee.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('dailyMaintenanceFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('dailyMaintenanceFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">租赁费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.rent.total"></InputNumber>
                <!--<span>{{postList.rent.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.rent.financialAid"></InputNumber>
                <!--<span>{{postList.rent.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.rent.otherAid"></InputNumber>
                <!--<span>{{postList.rent.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('rent')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('rent')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">物业管理费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.propertyManagementFee.total"></InputNumber>
                <!--<span>{{postList.propertyManagementFee.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.propertyManagementFee.financialAid"></InputNumber>
                <!--<span>{{postList.propertyManagementFee.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.propertyManagementFee.otherAid"></InputNumber>
                <!--<span>{{postList.propertyManagementFee.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('propertyManagementFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('propertyManagementFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">会议费(三类会议)</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.conferenceExpenseThree.total"></InputNumber>
                <!--<span>{{postList.conferenceExpenseThree.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.conferenceExpenseThree.financialAid"></InputNumber>
                <!--<span>{{postList.conferenceExpenseThree.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.conferenceExpenseThree.otherAid"></InputNumber>
                <!--<span>{{postList.conferenceExpenseThree.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('conferenceExpenseThree')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('conferenceExpenseThree')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">会议费(四类会议)</Col>
            <Col class="com-value" span="5">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              @on-change="setInputChange" readonly v-model="postList.conferenceExpenseFour.total"></InputNumber>
                <!--<span>{{postList.conferenceExpenseFour.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              @on-change="setInputChange" v-model="postList.conferenceExpenseFour.financialAid"></InputNumber>
                <!--<span>{{postList.conferenceExpenseFour.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              @on-change="setInputChange" v-model="postList.conferenceExpenseFour.otherAid"></InputNumber>
                <!--<span>{{postList.conferenceExpenseFour.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('conferenceExpenseFour')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('conferenceExpenseFour')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">培训费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                                            :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                            :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                            @on-change="setInputChange" v-model="postList.training.total"></InputNumber>
                <!--<span>{{postList.training.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.training.financialAid"></InputNumber>
                <!--<span>{{postList.training.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.training.otherAid"></InputNumber>
                <!--<span>{{postList.training.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('training')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('training')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">公务接待费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officialReceptionFee.total"></InputNumber>
                <!--<span>{{postList.officialReceptionFee.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officialReceptionFee.financialAid"></InputNumber>
                <!--<span>{{postList.officialReceptionFee.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officialReceptionFee.otherAid"></InputNumber>
                <!--<span>{{postList.officialReceptionFee.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('officialReceptionFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('officialReceptionFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">专用材料费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.specialCostOfMaterials.total"></InputNumber>
                <!--<span>{{postList.specialCostOfMaterials.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.specialCostOfMaterials.financialAid"></InputNumber>
                <!--<span>{{postList.specialCostOfMaterials.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.specialCostOfMaterials.otherAid"></InputNumber>
                <!--<span>{{postList.specialCostOfMaterials.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('specialCostOfMaterials')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('specialCostOfMaterials')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">被装购置费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.purchaseCostOfThePackage.total"></InputNumber>
                <!--<span>{{postList.purchaseCostOfThePackage.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.purchaseCostOfThePackage.financialAid"></InputNumber>
                <!--<span>{{postList.purchaseCostOfThePackage.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.purchaseCostOfThePackage.otherAid"></InputNumber>
                <!--<span>{{postList.purchaseCostOfThePackage.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('purchaseCostOfThePackage')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('purchaseCostOfThePackage')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">办公设备购置费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officeEquipmentPurchaseCost.total"></InputNumber>
                <!--<span>{{postList.officeEquipmentPurchaseCost.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officeEquipmentPurchaseCost.financialAid"></InputNumber>
                <!--<span>{{postList.officeEquipmentPurchaseCost.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officeEquipmentPurchaseCost.otherAid"></InputNumber>
                <!--<span>{{postList.officeEquipmentPurchaseCost.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('officeEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('officeEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">专用设备购置费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.specialEquipmentPurchaseCost.total"></InputNumber>
                <!--<span>{{postList.specialEquipmentPurchaseCost.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.specialEquipmentPurchaseCost.financialAid"></InputNumber>
                <!--<span>{{postList.specialEquipmentPurchaseCost.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.specialEquipmentPurchaseCost.otherAid"></InputNumber>
                <!--<span>{{postList.specialEquipmentPurchaseCost.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('specialEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('specialEquipmentPurchaseCost')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">其他资本性支出</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.otherCapitalExpenditures.total"></InputNumber>
                <!--<span>{{postList.otherCapitalExpenditures.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.otherCapitalExpenditures.financialAid"></InputNumber>
                <!--<span>{{postList.otherCapitalExpenditures.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.otherCapitalExpenditures.otherAid"></InputNumber>
                <!--<span>{{postList.otherCapitalExpenditures.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('otherCapitalExpenditures')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('otherCapitalExpenditures')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">其他资本性支出 ——图书资料购置费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.otherCapitalExpendituresBook.total"></InputNumber>
                <!--<span>{{postList.otherCapitalExpendituresBook.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.otherCapitalExpendituresBook.financialAid"></InputNumber>
                <!--<span>{{postList.otherCapitalExpendituresBook.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.otherCapitalExpendituresBook.otherAid"></InputNumber>
                <!--<span>{{postList.otherCapitalExpendituresBook.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('otherCapitalExpendituresBook')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('otherCapitalExpendituresBook')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">专用燃料费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.dedicatedFuelCharge.total"></InputNumber>
                <!--<span>{{postList.dedicatedFuelCharge.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.dedicatedFuelCharge.financialAid"></InputNumber>
                <!--<span>{{postList.dedicatedFuelCharge.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.dedicatedFuelCharge.otherAid"></InputNumber>
                <!--<span>{{postList.dedicatedFuelCharge.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('dedicatedFuelCharge')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('dedicatedFuelCharge')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5"> 劳务费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.labor.total"></InputNumber>
                <!--<span>{{postList.labor.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.labor.financialAid"></InputNumber>
                <!--<span>{{postList.labor.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.labor.otherAid"></InputNumber>
                <!--<span>{{postList.labor.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('labor')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('labor')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5"> 委托业务费</Col>
            <Col class="com-value" span="5">
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.commissionCharge.total"></InputNumber>-->
                <span>{{postList.commissionCharge.total}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.commissionCharge.financialAid"></InputNumber>-->
                <span>{{postList.commissionCharge.financialAid}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.commissionCharge.otherAid"></InputNumber>-->
                <span>{{postList.commissionCharge.otherAid}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<span>/</span>-->
                <span @click="editDetails('commissionCharge')" style="cursor: pointer;color: #0294E9">编辑</span>
                <span @click="getDetails('commissionCharge')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5">其他商品和服务支出</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.goodsAndServices.total"></InputNumber>
                <!--<span>{{postList.goodsAndServices.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.goodsAndServices.financialAid"></InputNumber>
                <!--<span>{{postList.goodsAndServices.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.goodsAndServices.otherAid"></InputNumber>
                <!--<span>{{postList.goodsAndServices.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('goodsAndServices')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('goodsAndServices')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-total" span="5">小计</Col>
            <Col class="com-total" span="5">
                {{postList.subtotal.total}}
            </Col>
            <Col class="com-total" span="4">
                {{postList.subtotal.financialAid}}
            </Col>
            <Col class="com-total" span="5">
                {{postList.subtotal.otherAid}}
            </Col>
            <Col class="com-total" span="5">
                <span>/</span>
            </Col>
            <Col class="com-value" span="5"> 工会经费（2%）</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.unionFunds.total"></InputNumber>
                <!--<span>{{postList.unionFunds.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.unionFunds.financialAid"></InputNumber>
                <!--<span>{{postList.unionFunds.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.unionFunds.otherAid"></InputNumber>
                <!--<span>{{postList.unionFunds.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('unionFunds')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('unionFunds')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">福利费（360元/人）</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.welfareFunds.total"></InputNumber>
                <!--<span>{{postList.welfareFunds.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                                            :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                            :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                            @on-change="setInputChange" v-model="postList.welfareFunds.financialAid"></InputNumber>
                <!--<span>{{postList.welfareFunds.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.welfareFunds.otherAid"></InputNumber>
                <!--<span>{{postList.welfareFunds.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('welfareFunds')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('welfareFunds')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">办公用房物业管理费</Col>
            <Col class="com-value" span="5">
                <!--<span>{{postList.officePremises.total}}</span>-->
                <InputNumber  class="value-input" :min="0" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              @on-change="setInputChange" v-model="postList.officePremises.total"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <!--<span>{{postList.officePremises.financialAid}}</span>-->
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              @on-change="setInputChange" v-model="postList.officePremises.financialAid"></InputNumber>
            </Col>
            <Col class="com-value" span="5">
                <!--<span>{{postList.officePremises.otherAid}}</span>-->
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              @on-change="setInputChange" v-model="postList.officePremises.otherAid"></InputNumber>
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('officePremises')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('officePremises')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">交通工具运行维护费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.maintenanceFee.total"></InputNumber>
                <!--<span>{{postList.maintenanceFee.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.maintenanceFee.financialAid"></InputNumber>
                <!--<span>{{postList.maintenanceFee.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.maintenanceFee.otherAid"></InputNumber>
                <!--<span>{{postList.maintenanceFee.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('maintenanceFee')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('maintenanceFee')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5" style="text-align: right">其中:公务用车运行维护费</Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeBus.total"></InputNumber>-->
                <span>{{postList.maintenanceFeeBus.total}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeBus.financialAid"></InputNumber>-->
                <span>{{postList.maintenanceFeeBus.financialAid}}</span>
            </Col>
            <Col class="com-value" span="5">
                <!--<InputNumber  class="value-input" :min="0" v-model="postList.maintenanceFeeBus.otherAid"></InputNumber>-->
                <span>{{postList.maintenanceFeeBus.otherAid}}</span>
            </Col>
            <Col class="com-value" span="5">
                <span @click="editDetails('maintenanceFeeBus')" style="cursor: pointer;color: #0294E9">编辑</span>
                <span @click="getDetails('maintenanceFeeBus')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>
            </Col>
            <Col class="com-value" span="5"><span style="position: relative;left: 60px">其中:其他交通费用</span></Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.maintenanceFeeOther.total" ></InputNumber>
                <!--<span>{{postList.maintenanceFeeOther.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.maintenanceFeeOther.financialAid" ></InputNumber>
                <!--<span>{{postList.maintenanceFeeOther.financialAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.maintenanceFeeOther.otherAid"></InputNumber>
                <!--<span>{{postList.maintenanceFeeOther.otherAid}}</span>-->
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('maintenanceFeeOther')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('maintenanceFeeOther')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-value" span="5">办公用房租赁费</Col>
            <Col class="com-value" span="5">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officeRent.total"></InputNumber>
                <!--<span>{{postList.officeRent.total}}</span>-->
            </Col>
            <Col class="com-value" span="4">
                <!--<span>{{postList.officeRent.financialAid}}</span>-->
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officeRent.financialAid"></InputNumber>
            </Col>
            <Col class="com-value" span="5">
                <!--<span>{{postList.officeRent.otherAid}}</span>-->
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" @on-change="setInputChange" v-model="postList.officeRent.otherAid"></InputNumber>
            </Col>
            <Col class="com-value" span="5">
                <span>/</span>
                <!--<span @click="editDetails('officeRent')" style="cursor: pointer;color: #0294E9">编辑</span>-->
                <!--<span @click="getDetails('officeRent')" style="cursor: pointer;color: #0294E9;margin-left: 15px">查看</span>-->
            </Col>
            <Col class="com-total" span="5">小计</Col>
            <Col class="com-total" span="5">
                {{postList.subtotalTwo.total}}
            </Col>
            <Col class="com-total" span="4">
                {{postList.subtotalTwo.financialAid}}
            </Col>
            <Col class="com-total" span="5">
                {{postList.subtotalTwo.otherAid}}
            </Col>
            <Col class="com-total" span="5">
                <span>/</span>
            </Col>
            <Col class="com-total"  span="5" >公用经费合计</Col>
            <Col class="com-total" span="5">
                {{postList.totalPublicFunds.total}}
            </Col>
            <Col class="com-total" span="4">
                {{postList.totalPublicFunds.financialAid}}
            </Col>
            <Col class="com-total" span="5">
                {{postList.totalPublicFunds.otherAid}}
            </Col>
            <Col class="com-total" span="5">
                <span>/</span>
            </Col>
        </Row>
        <!--提交-->
        <Button @click="sureSubmit" class="sure-btn" type="primary">确认</Button>
        <Drawer v-model="drawer"
                width=95%
                @on-close="drawerCancel"
                :mask-closable="false"
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col span="24" class="com-title">公用经费合计明细<span class="add-detail" @click="addItem" v-if="list!='maintenanceFeeBus'">新增明细</span></Col>
                <Table v-if="listPre=='officeDetailList'" :columns="tableColumns" :data="postList[listPre]" class="m-table" ref="table"  border>
                    <template  slot-scope="{ row,index }" slot="compositionDetails">
                        <Input type="text" :maxlength="30"  v-model="row.compositionDetails" v-if="list!='maintenanceFeeBus'"  class="value-input2"></Input>
                        <span v-if="list=='maintenanceFeeBus'">{{row.compositionDetails}}</span>
                    </template>
                    <template  slot-scope="{ row,index }" slot="specifications">
                        <Input type="text" :maxlength="30" v-model="row.specifications" class="value-input2"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="price">
                        <Input    v-model="row.price"  class="value-input2" @on-blur="getTotal(index,row)" @on-change="getChangeTotal($event,index)"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="number">
                        <Input    v-model="row.number"  class="value-input2" @on-blur="getTotal(index,row)" @on-change="getChangeTotal($event,index)"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="detailPrice">
                        <Input  v-model="row.detailPrice" readonly class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="projectGrant">
                        <Input type="text" :maxlength="50" v-model="row.projectGrant" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="unitReserve">
                        <Input type="text" :maxlength="50" v-model="row.unitReserve" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseItem">
                        <Input type="text" :maxlength="50" v-model="row.purchaseItem" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="governmentPurchaseMethod">
                        <Input type="text" :maxlength="50" v-model="row.governmentPurchaseMethod" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseContents">
                        <Input type="text" :maxlength="50" v-model="row.purchaseContents" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseMethod">
                        <Input type="text" :maxlength="50"  v-model="row.purchaseMethod" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="wasIndependentInnovation">
                        <RadioGroup v-model="row.wasIndependentInnovation" @on-change="setChange(index,row)">
                            <Radio  :label="1">是</Radio>
                            <Radio  :label="0">否</Radio>
                        </RadioGroup>
                    </template>
                    <template slot-scope="{ row,index }" slot="financialAid">
                        <InputNumber :min="0" v-model="row.financialAid"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     @on-blur="setChange(index,row)" class="value-input2"></InputNumber>
                    </template>
                    <template slot-scope="{ row,index }"  slot="otherAid">
                        <InputNumber :min="0" v-model="row.otherAid"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     @on-blur="setChange(index,row)" class="value-input2"></InputNumber>
                    </template>
                    <template slot-scope="{ row,index }" slot="total">
                        <span>{{row.total}}</span>
                        <!--<Input   v-model="row.total" readonly  class="value-input2"></Input>-->
                    </template>
                    <template slot-scope="{ row,index }" slot="remarks">
                        <Input type="text" :maxlength="200" v-model="row.remarks" @on-blur="setChange(index,row)" class="value-input2"></Input>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon2"  @click="deleteDetailItem(index)" v-if="list!='maintenanceFeeBus'">
                    </template>
                </Table>
                <Table v-if="listPre=='commissionChargeDetailList'" :columns="tableColumns" :data="postList[listPre]" class="m-table" ref="table"  border>
                    <template  slot-scope="{ row,index }" slot="compositionDetails">
                        <Input type="text" :maxlength="30"  v-model="row.compositionDetails" v-if="list!='maintenanceFeeBus'"  class="value-input2"></Input>
                        <span v-if="list=='maintenanceFeeBus'">{{row.compositionDetails}}</span>
                    </template>
                    <template  slot-scope="{ row,index }" slot="specifications">
                        <Input type="text" :maxlength="30" v-model="row.specifications" class="value-input2"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="price">
                        <Input    v-model="row.price"  class="value-input2" @on-blur="getTotal(index,row)" @on-change="getChangeTotal($event,index)"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="number">
                        <Input    v-model="row.number"  class="value-input2" @on-blur="getTotal(index,row)" @on-change="getChangeTotal($event,index)"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="detailPrice">
                        <Input  v-model="row.detailPrice" readonly class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="projectGrant">
                        <Input type="text" :maxlength="50" v-model="row.projectGrant" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="unitReserve">
                        <Input type="text" :maxlength="50" v-model="row.unitReserve" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseItem">
                        <Input type="text" :maxlength="50" v-model="row.purchaseItem" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="governmentPurchaseMethod">
                        <Input type="text" :maxlength="50" v-model="row.governmentPurchaseMethod" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseContents">
                        <Input type="text" :maxlength="50" v-model="row.purchaseContents" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseMethod">
                        <Input type="text" :maxlength="50"  v-model="row.purchaseMethod" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="wasIndependentInnovation">
                        <RadioGroup v-model="row.wasIndependentInnovation" @on-change="setChange(index,row)">
                            <Radio  :label="1">是</Radio>
                            <Radio  :label="0">否</Radio>
                        </RadioGroup>
                    </template>
                    <template slot-scope="{ row,index }" slot="financialAid">
                        <InputNumber :min="0" v-model="row.financialAid"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     @on-blur="setChange(index,row)" class="value-input2"></InputNumber>
                    </template>
                    <template slot-scope="{ row,index }"  slot="otherAid">
                        <InputNumber :min="0" v-model="row.otherAid"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     @on-blur="setChange(index,row)" class="value-input2"></InputNumber>
                    </template>
                    <template slot-scope="{ row,index }" slot="total">
                        <span>{{row.total}}</span>
                        <!--<Input   v-model="row.total" readonly  class="value-input2"></Input>-->
                    </template>
                    <template slot-scope="{ row,index }" slot="remarks">
                        <Input type="text" :maxlength="200" v-model="row.remarks" @on-blur="setChange(index,row)" class="value-input2"></Input>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon2"  @click="deleteDetailItem(index)" v-if="list!='maintenanceFeeBus'">
                    </template>
                </Table>
                <Table v-if="listPre=='maintenanceFeeBusDetailList'" :columns="tableColumns" :data="postList.maintenanceFeeBusDetailList" class="m-table" ref="table"  border>
                    <template  slot-scope="{ row,index }" slot="compositionDetails">
                        <Input type="text" :maxlength="30"  v-model="row.compositionDetails" v-if="list!='maintenanceFeeBus'"  class="value-input2"></Input>
                        <span v-if="list=='maintenanceFeeBus'">{{row.compositionDetails}}</span>
                    </template>
                    <template  slot-scope="{ row,index }" slot="specifications">
                        <Input type="text" :maxlength="30" v-model="row.specifications" class="value-input2"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="price">
                        <Input    v-model="row.price"  class="value-input2" @on-blur="getTotal(index,row)" @on-change="getChangeTotal($event,index)"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="number">
                        <Input    v-model="row.number"  class="value-input2" @on-blur="getTotal(index,row)" @on-change="getChangeTotal($event,index)"></Input>
                    </template>
                    <template  slot-scope="{ row,index }" slot="detailPrice">
                        <Input  v-model="row.detailPrice" readonly class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="projectGrant">
                        <Input type="text" :maxlength="50" v-model="row.projectGrant" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="unitReserve">
                        <Input type="text" :maxlength="50" v-model="row.unitReserve" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseItem">
                        <Input type="text" :maxlength="50" v-model="row.purchaseItem" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="governmentPurchaseMethod">
                        <Input type="text" :maxlength="50" v-model="row.governmentPurchaseMethod" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseContents">
                        <Input type="text" :maxlength="50" v-model="row.purchaseContents" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="purchaseMethod">
                        <Input type="text" :maxlength="50"  v-model="row.purchaseMethod" @on-blur="setChange(index,row)" class="value-input2"></Input>
                    </template>
                    <template slot-scope="{ row,index }" slot="wasIndependentInnovation">
                        <RadioGroup v-model="row.wasIndependentInnovation" @on-change="setChange(index,row)">
                            <Radio  :label="1">是</Radio>
                            <Radio  :label="0">否</Radio>
                        </RadioGroup>
                    </template>
                    <template slot-scope="{ row,index }" slot="financialAid">
                        <InputNumber :min="0" v-model="row.financialAid"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     @on-blur="setChange(index,row)" class="value-input2"></InputNumber>
                    </template>
                    <template slot-scope="{ row,index }"  slot="otherAid">
                        <InputNumber :min="0" v-model="row.otherAid"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     @on-blur="setChange(index,row)" class="value-input2"></InputNumber>
                    </template>
                    <template slot-scope="{ row,index }" slot="total">
                        <span>{{row.total}}</span>
                        <!--<Input   v-model="row.total" readonly  class="value-input2"></Input>-->
                    </template>
                    <template slot-scope="{ row,index }" slot="remarks">
                        <Input type="text" :maxlength="200" v-model="row.remarks" @on-blur="setChange(index,row)" class="value-input2"></Input>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon2"  @click="deleteDetailItem(index)" v-if="list!='maintenanceFeeBus'">
                    </template>
                </Table>
            </Row>
            <!--<Row class="common">-->
                <!--<Col span="24" class="com-title">公用经费合计明细<span class="add-detail" @click="addItem" v-if="list!='maintenanceFeeBus'">新增明细</span></Col>-->
                <!--<Col span="1" class="com-key">明细内容</Col>-->
                <!--<Col span="1" class="com-key">规格</Col>-->
                <!--<Col span="1" class="com-key">数量</Col>-->
                <!--<Col span="1" class="com-key">单价(元)</Col>-->
                <!--<Col span="2" class="com-key">明细金额(元)</Col>-->
                <!--<Col span="2" class="com-key">拨付方式</Col>-->
                <!--<Col span="2" class="com-key">中小企业预留</Col>-->
                <!--<Col span="2" class="com-key">采购品目</Col>-->
                <!--<Col span="2" class="com-key">政府采购形式</Col>-->
                <!--<Col span="1" class="com-key">采购目录</Col>-->
                <!--<Col span="1" class="com-key">采购方式</Col>-->
                <!--<Col span="2" class="com-key">是否自主创新</Col>-->
                <!--<Col span="2" class="com-key">财政补助收入(元)</Col>-->
                <!--<Col span="2" class="com-key">其他收入(元)</Col>-->
                <!--<Col span="1" class="com-key">总计(元)</Col>-->
                <!--<Col span="1" class="com-key">备注</Col>-->
                <!--<div v-for="(item,index) in  postList[listPre]">-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<Input type="text" :maxlength="30"  v-model="item.compositionDetails" v-if="list!='maintenanceFeeBus'"  readonly class="value-input" @on-focus="compositionDetailsGet(index,item.compositionDetails)"></Input>-->
                        <!--<span v-if="list=='maintenanceFeeBus'">{{item.compositionDetails}}</span>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<Input type="text" :maxlength="30" v-model="item.specifications" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<InputNumber :min="0" :max="999999999"  type="text" v-model="item.price"  class="value-input" @on-blur="getTotal(index)" @on-change="getChangeTotal($event,index)"></InputNumber>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<InputNumber :min="0" :max="999999" type="text" v-model="item.number"  class="value-input" @on-blur="getTotal(index)" @on-change="getChangeTotal($event,index)"></InputNumber>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<InputNumber :min="0" :max="999999999" v-model="item.detailPrice" readonly class="value-input"></InputNumber>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<Input type="text" :maxlength="50" v-model="item.projectGrant" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<Input type="text" :maxlength="50" v-model="item.unitReserve" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<Input type="text" :maxlength="50" v-model="item.purchaseItem" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<Input type="text" :maxlength="50" v-model="item.governmentPurchaseMethod" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<Input type="text" :maxlength="50" v-model="item.purchaseContents" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<Input type="text" :maxlength="50"  v-model="item.purchaseMethod" class="value-input"></Input>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<RadioGroup v-model="item.wasIndependentInnovation">-->
                            <!--<Radio  :label="1">是</Radio>-->
                            <!--<Radio  :label="0">否</Radio>-->
                        <!--</RadioGroup>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<InputNumber :min="0" :max="999999999" v-model="item.financialAid" class="value-input"></InputNumber>-->
                    <!--</Col>-->
                    <!--<Col span="2" class="com-value">-->
                        <!--<InputNumber :min="0" :max="999999999" v-model="item.otherAid" class="value-input"></InputNumber>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<InputNumber :min="0" :max="999999999"  v-model="item.total" readonly class="value-input"></InputNumber>-->
                    <!--</Col>-->
                    <!--<Col span="1" class="com-value">-->
                        <!--<Input type="text" :maxlength="200" v-model="item.remarks" class="value-input"></Input>-->
                        <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon"  @click="deleteDetailItem(index)" v-if="list!='maintenanceFeeBus'">-->
                    <!--</Col>-->
                <!--</div>-->

            <!--</Row>-->
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
                        <span :title="item.price">{{item.price}}</span>
                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.number">{{item.number}}</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.detailPrice">{{item.detailPrice}}</span>

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
                        <span :title="item.financialAid">{{item.financialAid}}</span>
                    </Col>
                    <Col span="2" class="com-value value-ellipsis">
                        <span :title="item.otherAid">{{item.otherAid}}</span>

                    </Col>
                    <Col span="1" class="com-value value-ellipsis">
                        <span :title="item.total">{{item.total}}</span>
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
        <Modal v-model="compositionDetailModal" :closable="false">
            <Input type="textarea"  v-model="compositionDetail" placeholder="请输入详细内容" clearable style="margin-top: 20px;"  />
            <div slot="footer">
                <Button type="primary" @click="compositionDetailEnsure">确定</Button>
            </div>
        </Modal>
    </div>
</template>

<script>
  // import { dragTable } from '../../utils/dragTable'
  export default {
    data() {
      return {
        drawer:false,
        viewDrawer:false,
        compositionDetailModal:false,
        compositionDetail:'',
        compositionDetailIndex:'',
        styles: {
          height: 'calc(100% - 55px)',
          overflow: 'auto',
          paddingBottom: '53px',
          position: 'static'
        },
        tableColumns:[
          {
            title:'明细内容',
            slot:'compositionDetails',
            resizable: true,
            width:200,
          },
          {
            title:'规格',
            slot:'specifications',
            width:100,
          },
          {
            title:'单价(元)',
            slot:'price',
            width:100,
          },
          {
            title:'数量',
            slot:'number',
            width:100,
          },
          {
            title:'明细金额',
            slot:'detailPrice',
            width:100,
          },
          {
            title:'拨付方式',
            slot:'projectGrant',
            width:100,
          },
          {
            title:'中小企业预留',
            slot:'unitReserve',
            width:100,
          },
          {
            title:'采购品目',
            slot:'purchaseItem',
            width:200,
          },
          {
            title:'政府采购形式',
            slot:'governmentPurchaseMethod',
            width:200,
          },
          {
            title:'采购目录',
            slot:'purchaseContents',
            width:100,
          },
          {
            title:'采购方式',
            slot:'purchaseMethod',
            width:100,
          },
          {
            title:'是否自主创新',
            slot:'wasIndependentInnovation',
            width:100,
          },
          {
            title:'财政补助收入(元)',
            slot:'financialAid',
            width:100,
          },
          {
            title:'其他收入(元)',
            slot:'otherAid',
            width:100,
          },
          {
            title:'总计(元)',
            slot:'total',
            width:100,
          },
          {
            title:'备注',
            slot:'remarks',
            marginRight:20,
            width:100,
          },
        ],
        tableData:[],
        modifyList:[],//取消时对应copy数组
        year:'',
        listPre:'',
        list:'',
        postList:{
          publicId:'',
          office:{
            total:0,
            financialAid:0,
            otherAid:0,
          },
          officeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": '',//明细金额
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
              "total": 0,//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          postFee:{
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
          },
          officialReceptionFeeDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": 0,//明细金额
              "projectGrant": "",//拨款方式
              "unitReserve": "",//中小企业预留
              "purchaseItem": "",//采购品目
              "governmentPurchaseMethod": "",//政府采购形式
              "purchaseContents": "",//采购目录
              "purchaseMethod": "",//采购方式
              "wasIndependentInnovation": '',//是否自主创新
              "total": 0,//总价
              "financialAid": '',//财政补助收入
              "otherAid": '',//其他收入
              "remarks": "",//备注
            }
          ],
          specialCostOfMaterials:{
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": '',//明细金额
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
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
              "compositionDetails": "汽油费",//构成明细
              "specifications": "",//规格型号
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": '',//明细金额
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
            },
            {
              "compositionDetails": "保险费",//构成明细
              "specifications": "",//规格型号
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": '',//明细金额
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
            },
            {
              "compositionDetails": "维修费",//构成明细
              "specifications": "",//规格型号
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": '',//明细金额
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
            },
          ],
          maintenanceFeeOther:{
            total:null,
            financialAid:null,
            otherAid:null,
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
            total:null,
            financialAid:null,
            otherAid:null,
          },
          officeRentDetailList:[
            {
              "compositionDetails": "",//构成明细
              "specifications": "",//规格型号
              "price": '',//单价
              "number":'' ,//数量
              "detailPrice": '',//明细金额
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
      // this.listPre = {
      //   "compositionDetails": "",//构成明细
      //   "specifications": "",//规格型号
      //   "price": '',//单价
      //   "number":'' ,//数量
      //   "detailPrice": '',//明细金额
      //   "projectGrant": "",//拨款方式
      //   "unitReserve": "",//中小企业预留
      //   "purchaseItem": "",//采购品目
      //   "governmentPurchaseMethod": "",//政府采购形式
      //   "purchaseContents": "",//采购目录
      //   "purchaseMethod": "",//采购方式
      //   "wasIndependentInnovation": '',//是否自主创新
      //   "total": '',//总价
      //   "financialAid": '',//财政补助收入
      //   "otherAid": '',//其他收入
      //   "remarks": "",//备注
      // }
      // this.$nextTick(() => {
      //   setTimeout(() => {
      //     iviewTableDrag();
      //   }, 1500);
      // });
      // let dom = this.$refs.table.$refs.header.getElementsByTagName("th");
      // dragTable(this,dom);
    },
    methods: {
      editDetails(item){
        this.drawer = true;
        let temp = item + 'DetailList';
        let temp2 = item;
        this.listPre = temp;
        this.list = temp2;
        this.modifyList = JSON.parse(JSON.stringify(this.postList[this.listPre]));
      },
      getDetails(item){
        this.viewDrawer = true;
        item += 'DetailList';
        this.listPre = item;
      },
      getFeeTotal(){
        this.postList.subtotalTwo.total = this.postList.unionFunds.total + this.postList.welfareFunds.total + this.postList.officePremises.total + this.postList.maintenanceFee.total +
          this.postList.maintenanceFeeBus.total + this.postList.maintenanceFeeOther.total + this.postList.officeRent.total;
        this.postList.subtotalTwo.financialAid = this.postList.unionFunds.financialAid + this.postList.welfareFunds.financialAid + this.postList.officePremises.financialAid + this.postList.maintenanceFee.financialAid +
          this.postList.maintenanceFeeBus.financialAid + this.postList.maintenanceFeeOther.financialAid + this.postList.officeRent.financialAid;
        this.postList.subtotalTwo.otherAid = this.postList.unionFunds.otherAid + this.postList.welfareFunds.otherAid + this.postList.officePremises.otherAid + this.postList.maintenanceFee.otherAid +
          this.postList.maintenanceFeeBus.otherAid + this.postList.maintenanceFeeOther.otherAid + this.postList.officeRent.otherAid;
        this.postList.totalPublicFunds.total = this.postList.subtotal.total + this.postList.subtotalTwo.total;
        this.postList.totalPublicFunds.financialAid = this.postList.subtotal.financialAid + this.postList.subtotalTwo.financialAid;
        this.postList.totalPublicFunds.otherAid = this.postList.subtotal.otherAid + this.postList.subtotalTwo.otherAid;
      },//其他交通费用总计失焦事件
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
      getChangeTotal(event,index){
        // this.getCheck(index)
        if(this.postList[this.listPre][index].price&&this.postList[this.listPre][index].number){
          this.postList[this.listPre][index].total = this.postList[this.listPre][index].number*this.postList[this.listPre][index].price;
          this.postList[this.listPre][index].detailPrice = this.postList[this.listPre][index].number*this.postList[this.listPre][index].price;
        }
      },
      getTotal(index,row){
        this.postList[this.listPre][index]=row;
        this.postList[this.listPre].splice(0,0);

        // this.getCheck(index)
        // if(this.postList[this.listPre][index].price&&this.postList[this.listPre][index].number){
          this.postList[this.listPre][index].total = this.postList[this.listPre][index].number*this.postList[this.listPre][index].price;
          this.postList[this.listPre][index].detailPrice = this.postList[this.listPre][index].number*this.postList[this.listPre][index].price;
        // this.postList.officeDetailList[index].total = this.postList.officeDetailList[index].number*this.postList.officeDetailList[index].price;
        // this.postList.officeDetailList[index].detailPrice = this.postList.officeDetailList[index].number*this.postList.officeDetailList[index].price;
      },
      setChange(index,row) {
        this.postList[this.listPre][index] = row;
        this.postList[this.listPre].splice(0, 0);
      },
      getAllCheck(list){
        list.forEach((item ,index)=>{
          if((list[index].otherAid==0&&list[index].financialAid==0)||list[index].financialAid||list[index].otherAid){
            let num = list[index].number*list[index].price;
            let num2 = Number(list[index].financialAid) + Number(list[index].otherAid);
            if(num!==num2){
              console.log(num,num2)
               this.$Message.error({content:'第'+(index+1)+'行数量与单价之积需与财政补助收入与其他收入之和相等',duration:5});
            }
          }
        })
      },
      dataTrue(item){
        return (((item.number*item.price)==(Number(item.financialAid) + Number(item.otherAid))))
      },
      handleOtherList(list){
        return list.every(this.dataTrue)
      },
      compositionDetailsGet(index,detail){
        console.log(detail)
        this.compositionDetailIndex = index;
        this.compositionDetail = detail;
        this.compositionDetailModal = true;
      },
      compositionDetailEnsure(){
        this.postList[this.listPre][this.compositionDetailIndex].compositionDetails = this.compositionDetail;
        this.compositionDetailModal = false;
      },
      drawerCancel(){
        this.drawer = false;
        this.postList[this.listPre] = this.modifyList;
      },
      drawerSave(){
        // console.log(this.postList[this.listPre])
        this.getAllCheck(this.postList[this.listPre]);
        if(this.handleOtherList(this.postList[this.listPre])){
          this.drawer = false;
          this.postList[this.list].total = this.postList[this.list].financialAid = this.postList[this.list].otherAid = 0;
          this.postList[this.listPre].forEach(item=>{
            console.log(this.postList[this.list].financialAid)
            this.postList[this.list].total += item.total;
            this.postList[this.list].financialAid += item.financialAid;
            this.postList[this.list].otherAid += item.otherAid;
          });
          this.postList.subtotal.total = Number(this.postList.office.total) + Number(this.postList.printingExpenses.total) + Number(this.postList.consultingFee.total) + Number(this.postList.poundage.total) +
            Number(this.postList.water.total) + Number(this.postList.electricity.total) + Number(this.postList.postFee.total) + Number(this.postList.travel.total) + Number(this.postList.abroadOnBusiness.total) +
            Number(this.postList.dailyMaintenanceFee.total) + Number(this.postList.rent.total) + Number(this.postList.propertyManagementFee.total) + Number(this.postList.conferenceExpenseThree.total) +
            Number(this.postList.conferenceExpenseFour.total) +Number(this.postList.training.total) + Number(this.postList.officialReceptionFee.total) + Number(this.postList.specialCostOfMaterials.total) + Number(this.postList.purchaseCostOfThePackage.total) +
            Number(this.postList.officeEquipmentPurchaseCost.total) + Number(this.postList.specialEquipmentPurchaseCost.total) +
            Number(this.postList.otherCapitalExpenditures.total) + Number(this.postList.otherCapitalExpendituresBook.total) + Number(this.postList.dedicatedFuelCharge.total) +
            Number(this.postList.labor.total) + Number(this.postList.commissionCharge.total) + Number(this.postList.goodsAndServices.total);
          this.postList.subtotal.financialAid = Number(this.postList.office.financialAid) + Number(this.postList.printingExpenses.financialAid) + Number(this.postList.consultingFee.financialAid) + Number(this.postList.poundage.financialAid) +
            Number(this.postList.water.financialAid) + Number(this.postList.electricity.financialAid) + Number(this.postList.postFee.financialAid) + Number(this.postList.travel.financialAid) + Number(this.postList.abroadOnBusiness.financialAid) +
            Number(this.postList.dailyMaintenanceFee.financialAid) + Number(this.postList.rent.financialAid) + Number(this.postList.propertyManagementFee.financialAid) + Number(this.postList.conferenceExpenseThree.financialAid) +
            Number(this.postList.conferenceExpenseFour.financialAid) +Number(this.postList.training.financialAid) + Number(this.postList.officialReceptionFee.financialAid) + Number(this.postList.specialCostOfMaterials.financialAid) + Number(this.postList.purchaseCostOfThePackage.financialAid) +
            Number(this.postList.officeEquipmentPurchaseCost.financialAid) + Number(this.postList.specialEquipmentPurchaseCost.financialAid) +
            Number(this.postList.otherCapitalExpenditures.financialAid) + Number(this.postList.otherCapitalExpendituresBook.financialAid) + Number(this.postList.dedicatedFuelCharge.total) +
            Number(this.postList.labor.financialAid) + Number(this.postList.commissionCharge.financialAid) + Number(this.postList.goodsAndServices.financialAid);
          this.postList.subtotal.otherAid = Number(this.postList.office.otherAid) + Number(this.postList.printingExpenses.otherAid) + Number(this.postList.consultingFee.otherAid) + Number(this.postList.poundage.otherAid) +
            Number(this.postList.water.otherAid) + Number(this.postList.electricity.otherAid) + Number(this.postList.postFee.otherAid) + Number(this.postList.travel.otherAid) + Number(this.postList.abroadOnBusiness.otherAid) +
            Number(this.postList.dailyMaintenanceFee.otherAid) + Number(this.postList.rent.otherAid) + Number(this.postList.propertyManagementFee.otherAid) + Number(this.postList.conferenceExpenseThree.otherAid) +
            Number(this.postList.conferenceExpenseFour.otherAid) +Number(this.postList.training.otherAid) + Number(this.postList.officialReceptionFee.otherAid) + Number(this.postList.specialCostOfMaterials.otherAid) + Number(this.postList.purchaseCostOfThePackage.otherAid) +
            Number(this.postList.officeEquipmentPurchaseCost.otherAid) + Number(this.postList.specialEquipmentPurchaseCost.otherAid) +
            Number(this.postList.otherCapitalExpenditures.otherAid) + Number(this.postList.otherCapitalExpendituresBook.otherAid) + Number(this.postList.dedicatedFuelCharge.otherAid) +
            Number(this.postList.labor.otherAid) + Number(this.postList.commissionCharge.otherAid) + Number(this.postList.goodsAndServices.otherAid);
          this.postList.subtotalTwo.total = Number(this.postList.unionFunds.total) + Number(this.postList.welfareFunds.total) + Number(this.postList.officePremises.total) + Number(this.postList.maintenanceFee.total) +
            Number(this.postList.maintenanceFeeBus.total) + Number(this.postList.maintenanceFeeOther.total) + Number(this.postList.officeRent.total);
          this.postList.subtotalTwo.financialAid = Number(this.postList.unionFunds.financialAid) + Number(this.postList.welfareFunds.financialAid) + Number(this.postList.officePremises.financialAid) + Number(this.postList.maintenanceFee.financialAid) +
            Number(this.postList.maintenanceFeeBus.financialAid) + Number(this.postList.maintenanceFeeOther.financialAid) + Number(this.postList.officeRent.financialAid);
          this.postList.subtotalTwo.otherAid = Number(this.postList.unionFunds.otherAid) + Number(this.postList.welfareFunds.otherAid) + Number(this.postList.officePremises.otherAid) + Number(this.postList.maintenanceFee.otherAid) +
            Number(this.postList.maintenanceFeeBus.otherAid) + Number(this.postList.maintenanceFeeOther.otherAid) + Number(this.postList.officeRent.otherAid);
          this.postList.totalPublicFunds.total = Number(this.postList.subtotal.total) + Number(this.postList.subtotalTwo.total);
          this.postList.totalPublicFunds.financialAid = Number(this.postList.subtotal.financialAid) + Number(this.postList.subtotalTwo.financialAid);
          this.postList.totalPublicFunds.otherAid = Number(this.postList.subtotal.otherAid) + Number(this.postList.subtotalTwo.otherAid);
        }
      },
      sureSubmit(){
        if(!this.year){
         this.$Message.error({content:'请填写预算年度',duration:5})
        }else {
          this.$http.get('/api/budgetManage/saveBudgetFundsPublicInfo?year='+this.year).then(res=>{
            if(res.messageCode==10000){
              this.postList.publicId = res.result.id;
              this.$http.post('/api/budgetManage/saveBudgetFundsPublicProject', this.postList).then(res => {
                if (res.messageCode == 10000) {
                  this.$Message.success(res.messageContent);
                  this.$router.push({name:'non-personnel-funds'})
                }else {
                  this.$Message.error(res.messageContent)
                }
              })
            }else {
              this.$Message.info(res.messageContent)
            }
          })
        }
      },
      getSubTotal(){
        //小计各项求和
        this.postList.office.total = this.postList.office.financialAid + this.postList.office.otherAid;
        this.postList.printingExpenses.total = this.postList.printingExpenses.financialAid + this.postList.printingExpenses.otherAid;
        this.postList.consultingFee.total = this.postList.consultingFee.financialAid + this.postList.consultingFee.otherAid;
        this.postList.poundage.total = this.postList.poundage.financialAid + this.postList.poundage.otherAid;
        this.postList.water.total = this.postList.water.financialAid + this.postList.water.otherAid;
        this.postList.electricity.total = this.postList.electricity.financialAid + this.postList.electricity.otherAid;
        this.postList.postFee.total = this.postList.postFee.financialAid + this.postList.postFee.otherAid;
        this.postList.travel.total = this.postList.travel.financialAid + this.postList.travel.otherAid;
        this.postList.abroadOnBusiness.total = this.postList.abroadOnBusiness.financialAid + this.postList.abroadOnBusiness.otherAid;
        this.postList.dailyMaintenanceFee.total = this.postList.dailyMaintenanceFee.financialAid + this.postList.dailyMaintenanceFee.otherAid;
        this.postList.rent.total = this.postList.rent.financialAid + this.postList.rent.otherAid;
        this.postList.propertyManagementFee.total = this.postList.propertyManagementFee.financialAid + this.postList.propertyManagementFee.otherAid;
        this.postList.conferenceExpenseThree.total = this.postList.conferenceExpenseThree.financialAid + this.postList.conferenceExpenseThree.otherAid;
        this.postList.conferenceExpenseFour.total = this.postList.conferenceExpenseFour.financialAid + this.postList.conferenceExpenseFour.otherAid;
        this.postList.training.total = this.postList.training.financialAid + this.postList.training.otherAid;
        this.postList.officialReceptionFee.total = this.postList.officialReceptionFee.financialAid + this.postList.officialReceptionFee.otherAid;
        this.postList.specialCostOfMaterials.total = this.postList.specialCostOfMaterials.financialAid + this.postList.specialCostOfMaterials.otherAid;
        this.postList.purchaseCostOfThePackage.total = this.postList.purchaseCostOfThePackage.financialAid + this.postList.purchaseCostOfThePackage.otherAid;
        this.postList.officeEquipmentPurchaseCost.total = this.postList.officeEquipmentPurchaseCost.financialAid + this.postList.officeEquipmentPurchaseCost.otherAid;
        this.postList.specialEquipmentPurchaseCost.total = this.postList.specialEquipmentPurchaseCost.financialAid + this.postList.specialEquipmentPurchaseCost.otherAid;
        this.postList.otherCapitalExpenditures.total = this.postList.otherCapitalExpenditures.financialAid + this.postList.otherCapitalExpenditures.otherAid;
        this.postList.otherCapitalExpendituresBook.total = this.postList.otherCapitalExpendituresBook.financialAid + this.postList.otherCapitalExpendituresBook.otherAid;
        this.postList.dedicatedFuelCharge.total = this.postList.dedicatedFuelCharge.financialAid + this.postList.dedicatedFuelCharge.otherAid;
        this.postList.labor.total = this.postList.labor.financialAid + this.postList.labor.otherAid;
        this.postList.commissionCharge.total = this.postList.commissionCharge.financialAid + this.postList.commissionCharge.otherAid;
        this.postList.goodsAndServices.total = this.postList.goodsAndServices.financialAid + this.postList.goodsAndServices.otherAid;
        //小计2各项求和
        this.postList.unionFunds.total = this.postList.unionFunds.financialAid + this.postList.unionFunds.otherAid;
        this.postList.welfareFunds.total = this.postList.welfareFunds.financialAid + this.postList.welfareFunds.otherAid;
        this.postList.officePremises.total = this.postList.officePremises.financialAid + this.postList.officePremises.otherAid;
        this.postList.maintenanceFee.total = this.postList.maintenanceFee.financialAid + this.postList.maintenanceFee.otherAid;
        this.postList.maintenanceFeeBus.total = this.postList.maintenanceFeeBus.financialAid + this.postList.maintenanceFeeBus.otherAid;
        this.postList.maintenanceFeeOther.total = this.postList.maintenanceFeeOther.financialAid + this.postList.maintenanceFeeOther.otherAid;
        this.postList.officeRent.total = this.postList.officeRent.financialAid + this.postList.officeRent.otherAid;

      },
      setInputChange(){
        this.getSubTotal();
        this.postList.subtotal.total = Number(this.postList.office.total) + Number(this.postList.printingExpenses.total) + Number(this.postList.consultingFee.total) + Number(this.postList.poundage.total) +
          Number(this.postList.water.total) + Number(this.postList.electricity.total) + Number(this.postList.postFee.total) + Number(this.postList.travel.total) + Number(this.postList.abroadOnBusiness.total) +
          Number(this.postList.dailyMaintenanceFee.total) + Number(this.postList.rent.total) + Number(this.postList.propertyManagementFee.total) + Number(this.postList.conferenceExpenseThree.total) +
          Number(this.postList.conferenceExpenseFour.total) +Number(this.postList.training.total) + Number(this.postList.officialReceptionFee.total) + Number(this.postList.specialCostOfMaterials.total) + Number(this.postList.purchaseCostOfThePackage.total) +
          Number(this.postList.officeEquipmentPurchaseCost.total) + Number(this.postList.specialEquipmentPurchaseCost.total) +
          Number(this.postList.otherCapitalExpenditures.total) + Number(this.postList.otherCapitalExpendituresBook.total) + Number(this.postList.dedicatedFuelCharge.total) +
          Number(this.postList.labor.total) + Number(this.postList.commissionCharge.total) + Number(this.postList.goodsAndServices.total);
        this.postList.subtotal.financialAid = Number(this.postList.office.financialAid) + Number(this.postList.printingExpenses.financialAid) + Number(this.postList.consultingFee.financialAid) + Number(this.postList.poundage.financialAid) +
          Number(this.postList.water.financialAid) + Number(this.postList.electricity.financialAid) + Number(this.postList.postFee.financialAid) + Number(this.postList.travel.financialAid) + Number(this.postList.abroadOnBusiness.financialAid) +
          Number(this.postList.dailyMaintenanceFee.financialAid) + Number(this.postList.rent.financialAid) + Number(this.postList.propertyManagementFee.financialAid) + Number(this.postList.conferenceExpenseThree.financialAid) +
          Number(this.postList.conferenceExpenseFour.financialAid) +Number(this.postList.training.financialAid) + Number(this.postList.officialReceptionFee.financialAid) + Number(this.postList.specialCostOfMaterials.financialAid) + Number(this.postList.purchaseCostOfThePackage.financialAid) +
          Number(this.postList.officeEquipmentPurchaseCost.financialAid) + Number(this.postList.specialEquipmentPurchaseCost.financialAid) +
          Number(this.postList.otherCapitalExpenditures.financialAid) + Number(this.postList.otherCapitalExpendituresBook.financialAid) + Number(this.postList.dedicatedFuelCharge.total) +
          Number(this.postList.labor.financialAid) + Number(this.postList.commissionCharge.financialAid) + Number(this.postList.goodsAndServices.financialAid);
        this.postList.subtotal.otherAid = Number(this.postList.office.otherAid) + Number(this.postList.printingExpenses.otherAid) + Number(this.postList.consultingFee.otherAid) + Number(this.postList.poundage.otherAid) +
          Number(this.postList.water.otherAid) + Number(this.postList.electricity.otherAid) + Number(this.postList.postFee.otherAid) + Number(this.postList.travel.otherAid) + Number(this.postList.abroadOnBusiness.otherAid) +
          Number(this.postList.dailyMaintenanceFee.otherAid) + Number(this.postList.rent.otherAid) + Number(this.postList.propertyManagementFee.otherAid) + Number(this.postList.conferenceExpenseThree.otherAid) +
          Number(this.postList.conferenceExpenseFour.otherAid) +Number(this.postList.training.otherAid) + Number(this.postList.officialReceptionFee.otherAid) + Number(this.postList.specialCostOfMaterials.otherAid) + Number(this.postList.purchaseCostOfThePackage.otherAid) +
          Number(this.postList.officeEquipmentPurchaseCost.otherAid) + Number(this.postList.specialEquipmentPurchaseCost.otherAid) +
          Number(this.postList.otherCapitalExpenditures.otherAid) + Number(this.postList.otherCapitalExpendituresBook.otherAid) + Number(this.postList.dedicatedFuelCharge.otherAid) +
          Number(this.postList.labor.otherAid) + Number(this.postList.commissionCharge.otherAid) + Number(this.postList.goodsAndServices.otherAid);
        this.postList.subtotalTwo.total = Number(this.postList.unionFunds.total) + Number(this.postList.welfareFunds.total) + Number(this.postList.officePremises.total) + Number(this.postList.maintenanceFee.total) +
          Number(this.postList.maintenanceFeeBus.total) + Number(this.postList.maintenanceFeeOther.total) + Number(this.postList.officeRent.total);
        this.postList.subtotalTwo.financialAid = Number(this.postList.unionFunds.financialAid) + Number(this.postList.welfareFunds.financialAid) + Number(this.postList.officePremises.financialAid) + Number(this.postList.maintenanceFee.financialAid) +
          Number(this.postList.maintenanceFeeBus.financialAid) + Number(this.postList.maintenanceFeeOther.financialAid) + Number(this.postList.officeRent.financialAid);
        this.postList.subtotalTwo.otherAid = Number(this.postList.unionFunds.otherAid) + Number(this.postList.welfareFunds.otherAid) + Number(this.postList.officePremises.otherAid) + Number(this.postList.maintenanceFee.otherAid) +
          Number(this.postList.maintenanceFeeBus.otherAid) + Number(this.postList.maintenanceFeeOther.otherAid) + Number(this.postList.officeRent.otherAid);
        this.postList.totalPublicFunds.total = Number(this.postList.subtotal.total) + Number(this.postList.subtotalTwo.total);
        this.postList.totalPublicFunds.financialAid = Number(this.postList.subtotal.financialAid) + Number(this.postList.subtotalTwo.financialAid);
        this.postList.totalPublicFunds.otherAid = Number(this.postList.subtotal.otherAid) + Number(this.postList.subtotalTwo.otherAid);
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
    .value-ellipsis{
        white-space: nowrap;
        text-overflow:ellipsis;
        overflow:hidden;
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
    .add-icon2{
        float: right;
        position: relative;
        top: -30px;
        left: 20px;
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
    .value-input2{
        width: 99%;
        text-align: center;
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