<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage/funds-detail">人员经费明细表(事业)</BreadcrumbItem>
                <BreadcrumbItem>档案详情</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'funds-detail'}"><div class="go-back">返回</div></router-link>
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
            <Col class="com-key" span="8">项目</Col>
            <Col class="com-key" span="4">总计(元)</Col>
            <Col class="com-key" span="4">财政补助收入（元）</Col>
            <Col class="com-key" span="4">其他收入（元）</Col>
            <Col class="com-key" span="4">备注</Col>
            <Col class="com-value" span="8">在职人员经费总计</Col>
            <Col class="com-value value-ellipsis" span="4">
                <span :title="postList.onJob.total">{{postList.onJob.totalValue}}</span>
                <!--<InputNumber  class="value-input" readonly :min="0" v-model="postList.onJob.total"></InputNumber>-->
            </Col>
            <Col class="com-value value-ellipsis" span="4">
                <span :title="postList.onJob.financialAid">{{postList.onJob.financialAidValue}}</span>
                <!--<InputNumber  class="value-input" readonly :min="0" v-model="postList.onJob.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value value-ellipsis" span="4">
                <span :title="postList.onJob.otherAid">{{postList.onJob.otherAidValue}}</span>
                <!--<InputNumber  class="value-input" readonly :min="0" v-model="postList.onJob.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value value-ellipsis" span="4">
                <span :title="postList.onJob.remarks">{{postList.onJob.remarks}}</span>
                <!--<Input type="textarea" class="value-input" readonly v-model="postList.onJob.remarks"></Input>-->
            </Col>
            <Col class="com-value" span="8">岗位工资</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.postSalary.total" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.postSalary.financialAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.postSalary.otherAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.postSalary.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">薪级工资</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.salaryRank.total" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.salaryRank.financialAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.salaryRank.otherAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.salaryRank.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">基本工资小计</Col>
            <Col class="com-value" span="4">
                <span>{{postList.subtotalOfBasicSalary.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="subtotalOfBasicSalary.financialAid"></InputNumber>-->
                <span>{{postList.subtotalOfBasicSalary.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="subtotalOfBasicSalary.financialAid"></InputNumber>-->
                <span>{{postList.subtotalOfBasicSalary.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<Input type="textarea" class="value-input" v-model="subtotalOfBasicSalary.remarks"></Input>-->
                <span>{{postList.subtotalOfBasicSalary.remarks}}</span>
            </Col>
            <Col class="com-value" span="8">上下班交通费补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.commutingAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.commutingAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.commutingAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.commutingAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">独生子女父母奖励费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.incentiveFeesForParentsOfOnlyChildren.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.incentiveFeesForParentsOfOnlyChildren.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.incentiveFeesForParentsOfOnlyChildren.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.incentiveFeesForParentsOfOnlyChildren.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">粮油补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.grainAndOilSubsidies.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.grainAndOilSubsidies.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.grainAndOilSubsidies.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.grainAndOilSubsidies.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">教龄津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.schoolAgeAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.schoolAgeAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.schoolAgeAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.schoolAgeAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">护龄津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.protectTheAgeAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.protectTheAgeAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.protectTheAgeAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.protectTheAgeAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">政府特殊津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.governmentSpecialAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.governmentSpecialAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.governmentSpecialAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.governmentSpecialAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">各类特殊岗位津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly  v-model="postList.allKindsOfSpecialPostAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.allKindsOfSpecialPostAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.allKindsOfSpecialPostAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.allKindsOfSpecialPostAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">选派青年志愿人员赴云南扶贫补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.yunnan.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.yunnan.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.yunnan.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.yunnan.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">选派干部赴西藏等省市补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.tibet.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.tibet.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.tibet.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.tibet.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">特级教师津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.specialTeacherAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.specialTeacherAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.specialTeacherAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.specialTeacherAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">支教人员津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.allowanceForVolunteerTeachers.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.allowanceForVolunteerTeachers.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.allowanceForVolunteerTeachers.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.allowanceForVolunteerTeachers.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">其他</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.other.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.other.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.other.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.other.remarks" style="position: relative;left: 17px"></Input>
                <img src="../../assets/icon/view-icon.png" @click="viewDrawer = true" alt="" class="view-icon">
                <!--<img src="../../assets/icon/modify-icon.png" @click="modifyOther" alt="" class="add-icon">-->
            </Col>
            <Col class="com-total" span="8">国家规定津补贴小计</Col>
            <Col class="com-total" span="4">
                <span>{{postList.countrySetsAllowanceSubtotal.totalValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.countrySetsAllowanceSubtotal.financialAidValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.countrySetsAllowanceSubtotal.otherAidValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.countrySetsAllowanceSubtotal.remarks}}</span>
            </Col>
            <Col class="com-value" span="8">绩效工资（一）</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.meritPayOne.total" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.meritPayOne.financialAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.meritPayOne.otherAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.meritPayOne.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">绩效工资（二）：高层次人才倾斜</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.meritPayTwo.total" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.meritPayTwo.financialAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.meritPayTwo.otherAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.meritPayTwo.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">绩效工资小计</Col>
            <Col class="com-total" span="4">
                <span>{{postList.meritPayTotal.totalValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.meritPayTotal.financialAidValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.meritPayTotal.otherAidValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.meritPayTotal.remarks}}</span>
            </Col>
            <Col class="com-value" span="8"> 职工养老保险16%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.employeePensionInsurance.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.employeePensionInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.employeePensionInsurance.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.employeePensionInsurance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">公积金7%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.accumulationFund.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.accumulationFund.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.accumulationFund.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.accumulationFund.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 失业保险费0.5%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.unemploymentInsurance.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.unemploymentInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.unemploymentInsurance.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.unemploymentInsurance.remarks"></Input>
            </Col>
            <!--<Col class="com-value" span="8">生育保险费1%</Col>-->
            <!--<Col class="com-value" span="4">-->
                <!--<InputNumber  class="value-input" :min="0" readonly v-model="postList.maternityInsurance.total" @on-blur="getOtherTotal"></InputNumber>-->
            <!--</Col>-->
            <!--<Col class="com-value" span="4">-->
                <!--<InputNumber  class="value-input" :min="0" readonly v-model="postList.maternityInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>-->
            <!--</Col>-->
            <!--<Col class="com-value" span="8">-->
                <!--<Input type="textarea" class="value-input" readonly v-model="postList.maternityInsurance.remarks"></Input>-->
            <!--</Col>-->
            <Col class="com-value" span="8"> 工伤保险费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.injuryInsurancePremium.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.injuryInsurancePremium.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.injuryInsurancePremium.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.injuryInsurancePremium.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 医疗保险费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.medicalInsurancePremium.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.medicalInsurancePremium.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.medicalInsurancePremium.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" v-model="postList.medicalInsurancePremium.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">  职业年金 8%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.occupationalPension.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.occupationalPension.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.occupationalPension.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.occupationalPension.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">其他小计</Col>
            <Col class="com-total" span="4">
                <span>{{postList.otherSmallGauge.totalValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.otherSmallGauge.financialAidValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.otherSmallGauge.otherAidValue}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{postList.otherSmallGauge.remarks}}</span>
            </Col>
            <Col class="com-value" span="8"> 临时工工资：经费（4800元/人）</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.wagesOfTemporaryWorkers.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.wagesOfTemporaryWorkers.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.wagesOfTemporaryWorkers.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.wagesOfTemporaryWorkers.remarks" style="position:relative;left: 15px"></Input>
                <img src="../../assets/icon/view-icon.png" @click="tempViewDrawer = true" alt="" class="view-icon">
                <!--<img src="../../assets/icon/modify-icon.png" @click="modifyTemp" alt="" class="add-icon">-->
            </Col>
            <Col class="com-value" span="8"> 事业单位离休人员补贴费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.retiredPersonnelSubsidyFee.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.retiredPersonnelSubsidyFee.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.retiredPersonnelSubsidyFee.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.retiredPersonnelSubsidyFee.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 离休人员护工费、护理费、电话费等</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.nursingFeesForRetiredPersonnel.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.nursingFeesForRetiredPersonnel.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.nursingFeesForRetiredPersonnel.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.nursingFeesForRetiredPersonnel.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 退休人员电话费等</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.retireePhoneBill.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.retireePhoneBill.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              readonly v-model="postList.retireePhoneBill.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" class="value-input" readonly v-model="postList.retireePhoneBill.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">总合计</Col>
            <Col class="com-value" span="4">
                <span>{{postList.totalAmount.totalValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.totalAmount.financialAidValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.totalAmount.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.totalAmount.remarks}}</span>
            </Col>
        </Row>
        <!--提交-->
        <!--<Button @click="sureSubmit" class="sure-btn" type="primary">确认</Button>-->
        <Drawer v-model="drawer"
                width=75%
                :closable="false"
                :mask-closable="false"
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col class="com-title" span="24">人员经费合计明细<span class="add-detail" @click="addItem">新增明细</span></Col>
                <Col class="com-key" span="4">数量</Col>
                <Col class="com-key" span="5">单价(元)</Col>
                <Col class="com-key" span="5">财政补助收入(元)</Col>
                <Col class="com-key" span="5">其他收入(元)</Col>
                <Col class="com-key" span="5">总计(元)</Col>
                <div v-for="(item,index) in postList.otherDetailList">
                    <Col class="com-value" span="4"><InputNumber :min="0" v-model="item.number" class="value-input" @on-blur="getTotal(index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" v-model="item.price" class="value-input" @on-blur="getTotal(index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" v-model="item.financialAid" class="value-input" @on-blur="getCheck(index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" v-model="item.otherAid" class="value-input" @on-blur="getCheck(index)"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" v-model="item.total" readonly class="value-input"></InputNumber>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="drawerCancel">取消</Button>
                <Button type="primary" @click="drawer = false">保存</Button>
            </div>
        </Drawer>
        <Drawer v-model="tempDrawer"
                width=75%
                :closable="false"
                :mask-closable="false"
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col class="com-title" span="24">人员经费合计明细<span class="add-detail" @click="addTempItem">新增明细</span></Col>
                <Col class="com-key" span="4">数量</Col>
                <Col class="com-key" span="5">单价(元)</Col>
                <Col class="com-key" span="5">财政补助收入(元)</Col>
                <Col class="com-key" span="5">其他收入(元)</Col>
                <Col class="com-key" span="5">总计(元)</Col>
                <div v-for="(item,index) in postList.wagesOfTemporaryWorkersDetailList">
                    <Col class="com-value" span="4"><InputNumber :min="0" v-model="item.number" class="value-input" @on-blur="getTempTotal(index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" v-model="item.price" class="value-input" @on-blur="getTempTotal(index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" v-model="item.financialAid" class="value-input" @on-blur="getTempCheck(index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" v-model="item.otherAid" class="value-input" @on-blur="getTempCheck(index)"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" v-model="item.total" readonly class="value-input"></InputNumber>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="tempDrawerCancel">取消</Button>
                <Button type="primary" @click="tempDrawer = false">保存</Button>
            </div>
        </Drawer>
        <Drawer v-model="viewDrawer"
                width=75%
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col class="com-title" span="24">人员经费合计明细
                    <!--<span class="add-detail" @click="addItem">新增明细</span>-->
                </Col>
                <Col class="com-key" span="4">数量</Col>
                <Col class="com-key" span="5">单价(元)</Col>
                <Col class="com-key" span="5">财政补助收入(元)</Col>
                <Col class="com-key" span="5">其他收入(元)</Col>
                <Col class="com-key" span="5">总计(元)</Col>
                <div v-for="(item,index) in postList.otherDetailList">
                    <Col class="com-value" span="4"><span>{{item.numberValue}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.priceValue}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.financialAidValue}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.otherAidValue}}</span></Col>
                    <Col class="com-value" span="5">
                        <span>{{item.totalValue}}</span>
                        <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">-->
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="viewDrawer = false">取消</Button>
                <!--<Button type="primary" >保存</Button>-->
            </div>
        </Drawer>
        <Drawer v-model="tempViewDrawer"
                width=75%
                :styles="styles">
            <div slot="header" class="d-header">明细</div>
            <Row class="common">
                <Col class="com-title" span="24">
                    人员经费合计明细
                    <!--<span class="add-detail" @click="addTempItem">新增明细</span>-->
                </Col>
                <Col class="com-key" span="4">数量</Col>
                <Col class="com-key" span="5">单价(元)</Col>
                <Col class="com-key" span="5">财政补助收入(元)</Col>
                <Col class="com-key" span="5">其他收入(元)</Col>
                <Col class="com-key" span="5">总计(元)</Col>
                <div v-for="(item,index) in postList.wagesOfTemporaryWorkersDetailList">
                    <Col class="com-value" span="4"><span>{{item.numberValue}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.priceValue}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.financialAidValue}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.otherAidValue}}</span></Col>
                    <Col class="com-value" span="5">
                        <span>{{item.totalValue}}</span>
                        <!--<img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">-->
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="tempViewDrawer = false">取消</Button>
                <!--<Button type="primary" >保存</Button>-->
            </div>
        </Drawer>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        postList:{
          //岗位工资
          onJob:{
            total:0,
            financialAid:0,
            remarks:""
          },
          postSalary:{
            total:0,
            financialAid:0,
            remarks:""
          },
          salaryRank:{
            total:0,
            financialAid:0,
            remarks:""
          },
          subtotalOfBasicSalary:{
            total:0,
            financialAid:0,
            remarks:""
          },

          //国家规定津补贴
          commutingAllowance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          incentiveFeesForParentsOfOnlyChildren:{
            total:0,
            financialAid:0,
            remarks:""
          },
          grainAndOilSubsidies:{
            total:0,
            financialAid:0,
            remarks:""
          },
          schoolAgeAllowance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          protectTheAgeAllowance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          governmentSpecialAllowance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          allKindsOfSpecialPostAllowance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          yunnan:{
            total:0,
            financialAid:0,
            remarks:""
          },
          tibet:{
            total:0,
            financialAid:0,
            remarks:""
          },
          specialTeacherAllowance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          allowanceForVolunteerTeachers:{
            total:0,
            financialAid:0,
            remarks:""
          },
          other:{
            total:0,
            financialAid:0,
            remarks:""
          },
          otherDetailList:[
            {total:0,price:0,financialAid:0,otherAid:0,number:0}
          ],
          countrySetsAllowanceSubtotal:{
            total:0,
            financialAid:0,
            remarks:""
          },

          //绩效工资
          meritPayOne:{
            total:0,
            financialAid:0,
            remarks:""
          },
          meritPayTwo:{
            total:0,
            financialAid:0,
            remarks:""
          },
          meritPayTotal:{
            total:0,
            financialAid:0,
            remarks:""
          },

          //其他小计
          employeePensionInsurance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          accumulationFund:{
            total:0,
            financialAid:0,
            remarks:""
          },
          unemploymentInsurance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          maternityInsurance:{
            total:0,
            financialAid:0,
            remarks:""
          },
          injuryInsurancePremium:{
            total:0,
            financialAid:0,
            remarks:""
          },
          medicalInsurancePremium:{
            total:0,
            financialAid:0,
            remarks:""
          },
          occupationalPension:{
            total:0,
            financialAid:0,
            remarks:""
          },
          otherSmallGauge:{
            total:0,
            financialAid:0,
            remarks:""
          },

          //总合计
          retiredPersonnelSubsidyFee:{
            total:0,
            financialAid:0,
            remarks:""
          },
          wagesOfTemporaryWorkers:{
            total:0,
            financialAid:0,
            remarks:""
          },
          wagesOfTemporaryWorkersDetailList:[
            {
              "number": 0,//数量
              "price": 0,//单价
              "financialAid": 0,//财政补助收入
              "otherAid": 0,//其他收入
              "total": 0//总价
            },
          ],
          nursingFeesForRetiredPersonnel:{
            total:0,
            financialAid:0,
            remarks:""
          },
          retireePhoneBill:{
            total:0,
            financialAid:0,
            remarks:""
          },
          totalAmount:{
            total:0,
            financialAid:0,
            remarks:""
          },
        },
        drawer:false,
        viewDrawer:false,
        tempDrawer:false,
        tempViewDrawer:false,
        styles: {
          height: 'calc(100% - 55px)',
          overflow: 'auto',
          paddingBottom: '53px',
          position: 'static'
        },
        //岗位工资
        onJob:{
          total:0,
          financialAid:0,
          remarks:""
        },
        postSalary:{
          total:0,
          financialAid:0,
          remarks:""
        },
        salaryRank:{
          total:0,
          financialAid:0,
          remarks:""
        },
        subtotalOfBasicSalary:{
          total:0,
          financialAid:0,
          remarks:""
        },

        //国家规定津补贴
        commutingAllowance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        incentiveFeesForParentsOfOnlyChildren:{
          total:0,
          financialAid:0,
          remarks:""
        },
        grainAndOilSubsidies:{
          total:0,
          financialAid:0,
          remarks:""
        },
        schoolAgeAllowance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        protectTheAgeAllowance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        governmentSpecialAllowance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        allKindsOfSpecialPostAllowance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        yunnan:{
          total:0,
          financialAid:0,
          remarks:""
        },
        tibet:{
          total:0,
          financialAid:0,
          remarks:""
        },
        specialTeacherAllowance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        allowanceForVolunteerTeachers:{
          total:0,
          financialAid:0,
          remarks:""
        },
        other:{
          total:0,
          financialAid:0,
          remarks:""
        },
        otherDetailList:[
          {total:0,price:0,financialAid:0,otherAid:0,number:0}
        ],
        countrySetsAllowanceSubtotal:{
          total:0,
          financialAid:0,
          remarks:""
        },

        //绩效工资
        meritPayOne:{
          total:0,
          financialAid:0,
          remarks:""
        },
        meritPayTwo:{
          total:0,
          financialAid:0,
          remarks:""
        },
        meritPayTotal:{
          total:0,
          financialAid:0,
          remarks:""
        },

        //其他小计
        employeePensionInsurance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        accumulationFund:{
          total:0,
          financialAid:0,
          remarks:""
        },
        unemploymentInsurance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        maternityInsurance:{
          total:0,
          financialAid:0,
          remarks:""
        },
        injuryInsurancePremium:{
          total:0,
          financialAid:0,
          remarks:""
        },
        medicalInsurancePremium:{
          total:0,
          financialAid:0,
          remarks:""
        },
        occupationalPension:{
          total:0,
          financialAid:0,
          remarks:""
        },
        otherSmallGauge:{
          total:0,
          financialAid:0,
          remarks:""
        },

        //总合计
        retiredPersonnelSubsidyFee:{
          total:0,
          financialAid:0,
          remarks:""
        },
        wagesOfTemporaryWorkers:{
          total:0,
          financialAid:0,
          remarks:""
        },
        wagesOfTemporaryWorkersDetailList:[
          {
            "number": 0,//数量
            "price": 0,//单价
            "financialAid": 0,//财政补助收入
            "otherAid": 0,//其他收入
            "total": 0//总价
          },
        ],
        nursingFeesForRetiredPersonnel:{
          total:0,
          financialAid:0,
          remarks:""
        },
        retireePhoneBill:{
          total:0,
          financialAid:0,
          remarks:""
        },
        totalAmount:{
          total:0,
          financialAid:0,
          remarks:""
        },


      }
    },
    mounted(){
      this.initList()
    },
    methods: {
      initList(){
        this.$http.get('/api/budgetManage/queryBudgetFundsPeopleDetail?peopleId='+this.$route.query.id).then(res=>{
          this.postList = res.result.budgetFundsPeopleDetail;
        })
      },
      modifyOther(){
        this.drawer = true;
      },
      getTotal(index){
        this.getCheck(index)
        if(this.otherDetailList[index].price&&this.otherDetailList[index].number){
          this.otherDetailList[index].total = this.otherDetailList[index].number*this.otherDetailList[index].price;
        }
      },
      getCheck(index){
        if(this.otherDetailList[index].financialAid&&this.otherDetailList[index].otherAid){
          let num = this.otherDetailList[index].number*this.otherDetailList[index].price;
          let num2 = this.otherDetailList[index].financialAid + this.otherDetailList[index].otherAid;
          if(num!==num2){
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      getTempTotal(index){
        this.getTempCheck(index);
        if(this.wagesOfTemporaryWorkersDetailList[index].price&&this.wagesOfTemporaryWorkersDetailList[index].number){
          this.wagesOfTemporaryWorkersDetailList[index].total = this.wagesOfTemporaryWorkersDetailList[index].number*this.wagesOfTemporaryWorkersDetailList[index].price;
        }
      },
      getTempCheck(index){
        if(this.wagesOfTemporaryWorkersDetailList[index].financialAid&&this.wagesOfTemporaryWorkersDetailList[index].otherAid){
          let num = this.wagesOfTemporaryWorkersDetailList[index].number*this.wagesOfTemporaryWorkersDetailList[index].price;
          let num2 = this.wagesOfTemporaryWorkersDetailList[index].financialAid + this.wagesOfTemporaryWorkersDetailList[index].otherAid;
          if(num!==num2){
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      getSalaryTotal(){
        this.subtotalOfBasicSalary.total = this.postSalary.total + this.salaryRank.total;
        this.subtotalOfBasicSalary.financialAid = this.postSalary.financialAid + this.salaryRank.financialAid;
      },
      getAllowanceTotal(){
        this.countrySetsAllowanceSubtotal.total = this.commutingAllowance.total +this.incentiveFeesForParentsOfOnlyChildren.total +this.grainAndOilSubsidies.total +
          this.schoolAgeAllowance.total +this.protectTheAgeAllowance.total + this.governmentSpecialAllowance.total + this.allKindsOfSpecialPostAllowance.total +
          this.yunnan.total + this.tibet.total + this.specialTeacherAllowance.total + this.allowanceForVolunteerTeachers.total + this.other.total;
        this.countrySetsAllowanceSubtotal.financialAid = this.commutingAllowance.financialAid +this.incentiveFeesForParentsOfOnlyChildren.financialAid +this.grainAndOilSubsidies.financialAid +
          this.schoolAgeAllowance.financialAid +this.protectTheAgeAllowance.financialAid + this.governmentSpecialAllowance.financialAid + this.allKindsOfSpecialPostAllowance.financialAid +
          this.yunnan.financialAid + this.tibet.financialAid + this.specialTeacherAllowance.financialAid + this.allowanceForVolunteerTeachers.financialAid + this.other.financialAid;
      },
      getMeritPayTotal(){
        this.meritPayTotal.total = this.meritPayOne.total + this.meritPayTwo.total;
        this.meritPayTotal.financialAid = this.meritPayOne.financialAid + this.meritPayTwo.financialAid;
      },
      getOtherTotal(){
        this.otherSmallGauge.total = this.employeePensionInsurance.total + this.accumulationFund.total + this.unemploymentInsurance.total + this.maternityInsurance.total+
          this.injuryInsurancePremium.total + this.medicalInsurancePremium.total + this.occupationalPension.total;
        this.otherSmallGauge.financialAid = this.employeePensionInsurance.financialAid + this.accumulationFund.financialAid + this.unemploymentInsurance.financialAid + this.maternityInsurance.financialAid+
          this.injuryInsurancePremium.financialAid + this.medicalInsurancePremium.financialAid + this.occupationalPension.financialAid;
      },
      getAmountTotal(){
        this.totalAmount.total = this.retiredPersonnelSubsidyFee.total + this.wagesOfTemporaryWorkers.total + this.nursingFeesForRetiredPersonnel.total + this.retireePhoneBill.total;
        this.totalAmount.financialAid = this.retiredPersonnelSubsidyFee.financialAid + this.wagesOfTemporaryWorkers.financialAid + this.nursingFeesForRetiredPersonnel.financialAid + this.retireePhoneBill.financialAid;
      },
      addItem(){
        if(this.otherDetailList.length>0){
          let num1 = this.otherDetailList[this.otherDetailList.length-1].number*this.otherDetailList[this.otherDetailList.length-1].price;
          let num2 = this.otherDetailList[this.otherDetailList.length-1].financialAid+this.otherDetailList[this.otherDetailList.length-1].otherAid;
          if(num1==num2){
            let obj = {};
            obj.number = 0;
            obj.price = 0;
            obj.financialAid = 0;
            obj.otherAid = 0;
            obj.total = 0
            this.otherDetailList.push(obj)
          }else {
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      deleteDetailItem(index){
        if(this.otherDetailList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.otherDetailList.splice(index,1)
        }
      },
      drawerCancel(){
        this.otherDetailList = [];
        let obj = {};
        obj.number = 0;
        obj.price = 0;
        obj.financialAid = 0;
        obj.otherAid = 0;
        obj.total = 0;
        this.otherDetailList.push(obj)
      },
      tempDrawerCancel(){
        this.wagesOfTemporaryWorkersDetailList = [];
        let obj = {};
        obj.number = 0;
        obj.price = 0;
        obj.financialAid = 0;
        obj.otherAid = 0;
        obj.total = 0;
        this.wagesOfTemporaryWorkersDetailList.push(obj)
      },
      modifyTemp(){
        this.tempDrawer = true;
      },
      addTempItem(){
        if(this.wagesOfTemporaryWorkersDetailList.length>0){
          let num1 = this.wagesOfTemporaryWorkersDetailList[this.wagesOfTemporaryWorkersDetailList.length-1].number*this.wagesOfTemporaryWorkersDetailList[this.wagesOfTemporaryWorkersDetailList.length-1].price;
          let num2 = this.wagesOfTemporaryWorkersDetailList[this.wagesOfTemporaryWorkersDetailList.length-1].financialAid+this.wagesOfTemporaryWorkersDetailList[this.wagesOfTemporaryWorkersDetailList.length-1].otherAid;
          if(num1==num2){
            let obj = {};
            obj.number = 0;
            obj.price = 0;
            obj.financialAid = 0;
            obj.otherAid = 0;
            obj.total = 0;
            this.wagesOfTemporaryWorkersDetailList.push(obj)
          }else {
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      deleteTempItem(index){
        if(this.wagesOfTemporaryWorkersDetailList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.wagesOfTemporaryWorkersDetailList.splice(index,1)
        }
      },
      sureSubmit(){
        let param = {
          "peopleId":this.$route.query.id,
          "onJob":this.onJob,
          "postSalary":this.postSalary,
          "salaryRank":this.salaryRank,
          "subtotalOfBasicSalary":this.subtotalOfBasicSalary,
          "commutingAllowance":this.commutingAllowance,
          "incentiveFeesForParentsOfOnlyChildren":this.incentiveFeesForParentsOfOnlyChildren,
          "grainAndOilSubsidies":this.grainAndOilSubsidies,
          "schoolAgeAllowance":this.schoolAgeAllowance,
          "protectTheAgeAllowance":this.protectTheAgeAllowance,
          "governmentSpecialAllowance":this.governmentSpecialAllowance,
          "allKindsOfSpecialPostAllowance":this.allKindsOfSpecialPostAllowance,
          "yunnan":this.yunnan,
          "tibet":this.tibet,
          "specialTeacherAllowance":this.specialTeacherAllowance,
          "allowanceForVolunteerTeachers":this.allowanceForVolunteerTeachers,
          "other":this.other,
          "otherDetailList":this.otherDetailList,
          "countrySetsAllowanceSubtotal":this.countrySetsAllowanceSubtotal,
          "meritPayOne":this.meritPayOne,
          "meritPayTwo":this.meritPayTwo,
          "meritPayTotal":this.meritPayTotal,
          "employeePensionInsurance":this.employeePensionInsurance,
          "accumulationFund":this.accumulationFund,
          "unemploymentInsurance":this.unemploymentInsurance,
          "maternityInsurance":this.maternityInsurance,
          "injuryInsurancePremium":this.injuryInsurancePremium,
          "medicalInsurancePremium":this.medicalInsurancePremium,
          "occupationalPension":this.occupationalPension,
          "otherSmallGauge":this.otherSmallGauge,
          "wagesOfTemporaryWorkers":this.wagesOfTemporaryWorkers,
          "wagesOfTemporaryWorkersDetailList":this.wagesOfTemporaryWorkersDetailList,
          "retiredPersonnelSubsidyFee":this.retiredPersonnelSubsidyFee,
          "nursingFeesForRetiredPersonnel":this.nursingFeesForRetiredPersonnel,
          "retireePhoneBill":this.retireePhoneBill,
          "totalAmount":this.totalAmount,
        }
        this.$http.post('/api/budgetManage/saveBudgetFundsPeopleProjectDetail',param).then(res=>{
          this.$Message.success(res.messageContent);
          this.$router.push({name:'funds-detail'});
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
    .add-icon{
        float: right;
        position: relative;
        top: 15px;
        left: 35px;
        cursor: pointer;
    }
    .view-icon{
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
    .add-detail{
        float: right;
        margin-right: 15px;
        cursor: pointer;
        color: #0294e9;
    }
    .value-input{
        width: 90%;
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