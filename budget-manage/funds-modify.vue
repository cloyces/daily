<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage/funds-detail">人员经费明细表(事业)</BreadcrumbItem>
                <BreadcrumbItem>档案修改</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'funds-detail'}"><div class="go-back">返回</div></router-link>
        </div>
        <!--表单信息-->
        <Row class="common">
            <Col class="com-title">
                <div>基本信息</div>
            </Col>
            <Col class="com-key" span="8">项目</Col>
            <Col class="com-key" span="4">总计(元)</Col>
            <Col class="com-key" span="4">财政补助收入（元）</Col>
            <Col class="com-key" span="4">其他收入（元）</Col>
            <Col class="com-key" span="4">备注</Col>
            <Col class="com-value" span="8">在职人员经费总计</Col>
            <Col class="com-value" span="4">
                <span>{{postList.onJob.totalValue}}</span>
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.onJob.total"></InputNumber>-->
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.onJob.financialAidValue}}</span>
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.onJob.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.onJob.otherAidValue}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{postList.onJob.remarks}}</span>
                <!--<Input type="textarea" :maxlength="200" class="value-input" v-model="postList.onJob.remarks"></Input>-->
            </Col>
            <Col class="com-value" span="8">岗位工资</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postList.postSalary.total" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postList.postSalary.financialAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postList.postSalary.otherAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.postSalary.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">薪级工资</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postList.salaryRank.total" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postList.salaryRank.financialAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postList.salaryRank.otherAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.salaryRank.remarks"></Input>
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
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.commutingAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.commutingAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.commutingAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.commutingAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">独生子女父母奖励费</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.incentiveFeesForParentsOfOnlyChildren.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.incentiveFeesForParentsOfOnlyChildren.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.incentiveFeesForParentsOfOnlyChildren.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.incentiveFeesForParentsOfOnlyChildren.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">粮油补贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.grainAndOilSubsidies.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.grainAndOilSubsidies.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.grainAndOilSubsidies.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.grainAndOilSubsidies.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">教龄津贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.schoolAgeAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.schoolAgeAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.schoolAgeAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.schoolAgeAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">护龄津贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.protectTheAgeAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.protectTheAgeAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.protectTheAgeAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.protectTheAgeAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">政府特殊津贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.governmentSpecialAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.governmentSpecialAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.governmentSpecialAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.governmentSpecialAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">各类特殊岗位津贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.allKindsOfSpecialPostAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.allKindsOfSpecialPostAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.allKindsOfSpecialPostAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.allKindsOfSpecialPostAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">选派青年志愿人员赴云南扶贫补贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.yunnan.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.yunnan.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.yunnan.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.yunnan.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">选派干部赴西藏等省市补贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.tibet.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.tibet.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.tibet.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.tibet.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">特级教师津贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.specialTeacherAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.specialTeacherAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.specialTeacherAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.specialTeacherAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">支教人员津贴</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.allowanceForVolunteerTeachers.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.allowanceForVolunteerTeachers.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.allowanceForVolunteerTeachers.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.allowanceForVolunteerTeachers.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">其他</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.other.total" readonly @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.other.financialAid" readonly @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.other.otherAid" readonly @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.other.remarks" style="position: relative;left: 17px"></Input>
                <img src="../../assets/icon/view-icon.png" @click="viewDrawer = true" alt="" class="view-icon">
                <img src="../../assets/icon/modify-icon.png" @click="modifyOther" alt="" class="add-icon">
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
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.meritPayOne.total" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.meritPayOne.financialAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.meritPayOne.otherAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.meritPayOne.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">绩效工资（二）：高层次人才倾斜</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.meritPayTwo.total" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.meritPayTwo.financialAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.meritPayTwo.otherAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.meritPayTwo.remarks"></Input>
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
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.employeePensionInsurance.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.employeePensionInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.employeePensionInsurance.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.employeePensionInsurance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">公积金7%</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.accumulationFund.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.accumulationFund.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.accumulationFund.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.accumulationFund.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 失业保险费0.5%</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.unemploymentInsurance.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.unemploymentInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.unemploymentInsurance.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.unemploymentInsurance.remarks"></Input>
            </Col>
            <!--<Col class="com-value" span="8">生育保险费1%</Col>-->
            <!--<Col class="com-value" span="4">-->
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.maternityInsurance.total" @on-blur="getOtherTotal"></InputNumber>-->
            <!--</Col>-->
            <!--<Col class="com-value" span="4">-->
                <!--              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.maternityInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>-->
            <!--</Col>-->
            <!--<Col class="com-value" span="8">-->
                <!--<Input type="textarea" :maxlength="200" class="value-input" v-model="postList.maternityInsurance.remarks"></Input>-->
            <!--</Col>-->
            <Col class="com-value" span="8"> 工伤保险费</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.injuryInsurancePremium.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.injuryInsurancePremium.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.injuryInsurancePremium.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.injuryInsurancePremium.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 医疗保险费</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.medicalInsurancePremium.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.medicalInsurancePremium.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.medicalInsurancePremium.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.medicalInsurancePremium.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">  职业年金 8%</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.occupationalPension.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"  :max="999999999" v-model="postList.occupationalPension.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0"  :max="999999999" v-model="postList.occupationalPension.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.occupationalPension.remarks"></Input>
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
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.wagesOfTemporaryWorkers.total" readonly @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.wagesOfTemporaryWorkers.financialAid" readonly @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.wagesOfTemporaryWorkers.otherAid" readonly @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.wagesOfTemporaryWorkers.remarks" style="position:relative;left: 15px"></Input>
                <img src="../../assets/icon/view-icon.png" @click="tempViewDrawer = true" alt="" class="view-icon">
                <img src="../../assets/icon/modify-icon.png" @click="modifyTemp" alt="" class="add-icon">
            </Col>
            <Col class="com-value" span="8"> 事业单位离休人员补贴费</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                                            readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.retiredPersonnelSubsidyFee.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.retiredPersonnelSubsidyFee.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.retiredPersonnelSubsidyFee.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.retiredPersonnelSubsidyFee.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 离休人员护工费、护理费、电话费等</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.nursingFeesForRetiredPersonnel.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.nursingFeesForRetiredPersonnel.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.nursingFeesForRetiredPersonnel.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.nursingFeesForRetiredPersonnel.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 退休人员电话费等</Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999" readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"  v-model="postList.retireePhoneBill.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                              <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.retireePhoneBill.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')" v-model="postList.retireePhoneBill.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postList.retireePhoneBill.remarks"></Input>
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
        <Button @click="sureSubmit" class="sure-btn" type="primary">确认</Button>
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
                    <Col class="com-value" span="4"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.number" class="value-input" @on-blur="getTotal(index)" @on-change="getChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.price" class="value-input" @on-blur="getTotal(index)" @on-change="getChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.financialAid" class="value-input"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.otherAid" class="value-input"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" :max="999999999"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     v-model="item.total" readonly class="value-input"></InputNumber>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="drawerCancel">取消</Button>
                <Button type="primary" @click="drawerSave">保存</Button>
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
                    <Col class="com-value" span="4"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.number" class="value-input" @on-blur="getTempTotal(index)" @on-change="getTempChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.price" class="value-input" @on-blur="getTempTotal(index)" @on-change="getTempChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.financialAid" class="value-input"></InputNumber></Col>
                    <Col class="com-value" span="5"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.otherAid" class="value-input"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" :max="999999999"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     v-model="item.total" readonly class="value-input"></InputNumber>
                        <img src="../../assets/icon/delete-icon.png"  alt="" class="add-icon" @click="deleteDetailItem(index)">
                    </Col>
                </div>
            </Row>
            <div  class="d-footer">
                <Button type="default" @click="tempDrawerCancel">取消</Button>
                <Button type="primary" @click="tempDrawerSave">保存</Button>
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
        year:'',
        postList:{
          "peopleId":'',
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
        modifyObj:'',//copy取消对象
        modifyTempObj:'',//copy取消对象
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
          // this.postList.peopleId = this.$route.query.id;
        })
      },
      modifyOther(){
        this.modifyObj = JSON.parse(JSON.stringify(this.postList.otherDetailList));
        this.drawer = true;
      },
      getChangeTotal(event,index){
        this.getCheck(index)
        if(this.postList.otherDetailList[index].price&&this.postList.otherDetailList[index].number){
          this.postList.otherDetailList[index].total = this.postList.otherDetailList[index].number*this.postList.otherDetailList[index].price;
        }
      },
      getTotal(index){
        this.getCheck(index)
        if(this.postList.otherDetailList[index].price&&this.postList.otherDetailList[index].number){
          this.postList.otherDetailList[index].total = this.postList.otherDetailList[index].number*this.postList.otherDetailList[index].price;
        }
      },
      getCheck(index){
        if(this.postList.otherDetailList[index].financialAid&&this.postList.otherDetailList[index].otherAid){
          let num = this.postList.otherDetailList[index].number*this.postList.otherDetailList[index].price;
          let num2 = this.postList.otherDetailList[index].financialAid + this.postList.otherDetailList[index].otherAid;
          if(num!==num2){
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      getTempChangeTotal(event,index){
        this.getTempCheck(index);
        if(this.postList.wagesOfTemporaryWorkersDetailList[index].price&&this.postList.wagesOfTemporaryWorkersDetailList[index].number){
          this.postList.wagesOfTemporaryWorkersDetailList[index].total = this.postList.wagesOfTemporaryWorkersDetailList[index].number*this.postList.wagesOfTemporaryWorkersDetailList[index].price;
        }
      },
      getTempTotal(index){
        this.getTempCheck(index);
        if(this.postList.wagesOfTemporaryWorkersDetailList[index].price&&this.postList.wagesOfTemporaryWorkersDetailList[index].number){
          this.postList.wagesOfTemporaryWorkersDetailList[index].total = this.postList.wagesOfTemporaryWorkersDetailList[index].number*this.postList.wagesOfTemporaryWorkersDetailList[index].price;
        }
      },
      getTempCheck(index){
        if(this.postList.wagesOfTemporaryWorkersDetailList[index].financialAid&&this.postList.wagesOfTemporaryWorkersDetailList[index].otherAid){
          let num = this.postList.wagesOfTemporaryWorkersDetailList[index].number*this.postList.wagesOfTemporaryWorkersDetailList[index].price;
          let num2 = this.postList.wagesOfTemporaryWorkersDetailList[index].financialAid + this.postList.wagesOfTemporaryWorkersDetailList[index].otherAid;
          if(num!==num2){
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      getSalaryTotal(){
        this.postList.postSalary.total = this.postList.postSalary.financialAid + this.postList.postSalary.otherAid;
        this.postList.salaryRank.total = this.postList.salaryRank.financialAid + this.postList.salaryRank.otherAid;
        console.log(this.postList.postSalary.total)
        this.postList.subtotalOfBasicSalary.total = this.postList.postSalary.total + this.postList.salaryRank.total;
        this.postList.subtotalOfBasicSalary.financialAid = this.postList.postSalary.financialAid + this.postList.salaryRank.financialAid;
        this.postList.subtotalOfBasicSalary.otherAid = this.postList.postSalary.otherAid + this.postList.salaryRank.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getAllowanceTotal(){
        //国家津贴各项总计计算
        this.postList.commutingAllowance.total = this.postList.commutingAllowance.financialAid + this.postList.commutingAllowance.otherAid;
        this.postList.incentiveFeesForParentsOfOnlyChildren.total = this.postList.incentiveFeesForParentsOfOnlyChildren.financialAid + this.postList.incentiveFeesForParentsOfOnlyChildren.otherAid;
        this.postList.grainAndOilSubsidies.total = this.postList.grainAndOilSubsidies.financialAid + this.postList.grainAndOilSubsidies.otherAid;
        this.postList.schoolAgeAllowance.total = this.postList.schoolAgeAllowance.financialAid + this.postList.schoolAgeAllowance.otherAid;
        this.postList.protectTheAgeAllowance.total = this.postList.protectTheAgeAllowance.financialAid + this.postList.protectTheAgeAllowance.otherAid;
        this.postList.governmentSpecialAllowance.total = this.postList.governmentSpecialAllowance.financialAid + this.postList.governmentSpecialAllowance.otherAid;
        this.postList.allKindsOfSpecialPostAllowance.total = this.postList.allKindsOfSpecialPostAllowance.financialAid + this.postList.allKindsOfSpecialPostAllowance.otherAid;
        this.postList.yunnan.total = this.postList.yunnan.financialAid + this.postList.yunnan.otherAid;
        this.postList.tibet.total = this.postList.tibet.financialAid + this.postList.tibet.otherAid;
        this.postList.specialTeacherAllowance.total = this.postList.specialTeacherAllowance.financialAid + this.postList.specialTeacherAllowance.otherAid;
        this.postList.allowanceForVolunteerTeachers.total = this.postList.allowanceForVolunteerTeachers.financialAid + this.postList.allowanceForVolunteerTeachers.otherAid;
        this.postList.other.total = this.postList.other.financialAid + this.postList.other.otherAid;
        //国家津贴小计
        this.postList.countrySetsAllowanceSubtotal.total = this.postList.commutingAllowance.total +this.postList.incentiveFeesForParentsOfOnlyChildren.total +this.postList.grainAndOilSubsidies.total +
          this.postList.schoolAgeAllowance.total +this.postList.protectTheAgeAllowance.total + this.postList.governmentSpecialAllowance.total + this.postList.allKindsOfSpecialPostAllowance.total +
          this.postList.yunnan.total + this.postList.tibet.total + this.postList.specialTeacherAllowance.total + this.postList.allowanceForVolunteerTeachers.total + this.postList.other.total;
        this.postList.countrySetsAllowanceSubtotal.financialAid = this.postList.commutingAllowance.financialAid +this.postList.incentiveFeesForParentsOfOnlyChildren.financialAid +this.postList.grainAndOilSubsidies.financialAid +
          this.postList.schoolAgeAllowance.financialAid +this.postList.protectTheAgeAllowance.financialAid + this.postList.governmentSpecialAllowance.financialAid + this.postList.allKindsOfSpecialPostAllowance.financialAid +
          this.postList.yunnan.financialAid + this.postList.tibet.financialAid + this.postList.specialTeacherAllowance.financialAid + this.postList.allowanceForVolunteerTeachers.financialAid + this.postList.other.financialAid;
        this.postList.countrySetsAllowanceSubtotal.otherAid = this.postList.commutingAllowance.otherAid +this.postList.incentiveFeesForParentsOfOnlyChildren.otherAid +this.postList.grainAndOilSubsidies.otherAid +
          this.postList.schoolAgeAllowance.otherAid +this.postList.protectTheAgeAllowance.otherAid + this.postList.governmentSpecialAllowance.otherAid + this.postList.allKindsOfSpecialPostAllowance.otherAid +
          this.postList.yunnan.otherAid + this.postList.tibet.otherAid + this.postList.specialTeacherAllowance.otherAid + this.postList.allowanceForVolunteerTeachers.otherAid + this.postList.other.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getMeritPayTotal(){
        //绩效工资小计各项计算
        this.postList.meritPayOne.total = this.postList.meritPayOne.financialAid + this.postList.meritPayOne.otherAid;
        this.postList.meritPayTwo.total = this.postList.meritPayTwo.financialAid + this.postList.meritPayTwo.otherAid;
        //绩效工资小计
        this.postList.meritPayTotal.total = this.postList.meritPayOne.total + this.postList.meritPayTwo.total;
        this.postList.meritPayTotal.financialAid = this.postList.meritPayOne.financialAid + this.postList.meritPayTwo.financialAid;
        this.postList.meritPayTotal.otherAid = this.postList.meritPayOne.otherAid + this.postList.meritPayTwo.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getOtherTotal(){
        //其他小计各项计算
        this.postList.employeePensionInsurance.total = this.postList.employeePensionInsurance.financialAid + this.postList.employeePensionInsurance.otherAid;
        this.postList.accumulationFund.total = this.postList.accumulationFund.financialAid + this.postList.accumulationFund.otherAid;
        this.postList.unemploymentInsurance.total = this.postList.unemploymentInsurance.financialAid + this.postList.unemploymentInsurance.otherAid;
        this.postList.maternityInsurance.total = this.postList.maternityInsurance.financialAid + this.postList.maternityInsurance.otherAid;
        this.postList.injuryInsurancePremium.total = this.postList.injuryInsurancePremium.financialAid + this.postList.injuryInsurancePremium.otherAid;
        this.postList.medicalInsurancePremium.total = this.postList.medicalInsurancePremium.financialAid + this.postList.medicalInsurancePremium.otherAid;
        this.postList.occupationalPension.total = this.postList.occupationalPension.financialAid + this.postList.occupationalPension.otherAid;
        //其他小计
        this.postList.otherSmallGauge.total = this.postList.employeePensionInsurance.total + this.postList.accumulationFund.total + this.postList.unemploymentInsurance.total + this.postList.maternityInsurance.total+
          this.postList.injuryInsurancePremium.total + this.postList.medicalInsurancePremium.total + this.postList.occupationalPension.total;
        this.postList.otherSmallGauge.financialAid = this.postList.employeePensionInsurance.financialAid + this.postList.accumulationFund.financialAid + this.postList.unemploymentInsurance.financialAid + this.postList.maternityInsurance.financialAid+
          this.postList.injuryInsurancePremium.financialAid + this.postList.medicalInsurancePremium.financialAid + this.postList.occupationalPension.financialAid;
        this.postList.otherSmallGauge.otherAid = this.postList.employeePensionInsurance.otherAid + this.postList.accumulationFund.otherAid + this.postList.unemploymentInsurance.otherAid + this.postList.maternityInsurance.otherAid+
          this.postList.injuryInsurancePremium.otherAid + this.postList.medicalInsurancePremium.otherAid + this.postList.occupationalPension.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getOnJobTotal(){
        this.postList.onJob.total =  this.postList.otherSmallGauge.total + this.postList.meritPayTotal.total + this.postList.countrySetsAllowanceSubtotal.total + this.postList.subtotalOfBasicSalary.total;
        this.postList.onJob.financialAid = this.postList.otherSmallGauge.financialAid + this.postList.meritPayTotal.financialAid + this.postList.countrySetsAllowanceSubtotal.financialAid + this.postList.subtotalOfBasicSalary.financialAid;
        this.postList.onJob.otherAid = this.postList.otherSmallGauge.otherAid + this.postList.meritPayTotal.otherAid + this.postList.countrySetsAllowanceSubtotal.otherAid + this.postList.subtotalOfBasicSalary.otherAid;
      },
      getAmountTotal(){
        //总合计各项小计
        this.postList.retiredPersonnelSubsidyFee.total = this.postList.retiredPersonnelSubsidyFee.financialAid + this.postList.retiredPersonnelSubsidyFee.otherAid;
        this.postList.wagesOfTemporaryWorkers.total = this.postList.wagesOfTemporaryWorkers.financialAid + this.postList.wagesOfTemporaryWorkers.otherAid;
        this.postList.nursingFeesForRetiredPersonnel.total = this.postList.nursingFeesForRetiredPersonnel.financialAid + this.postList.nursingFeesForRetiredPersonnel.otherAid;
        this.postList.retireePhoneBill.total = this.postList.retireePhoneBill.financialAid + this.postList.retireePhoneBill.otherAid;
        //总合计
        this.postList.totalAmount.total = this.postList.retiredPersonnelSubsidyFee.total + this.postList.wagesOfTemporaryWorkers.total + this.postList.nursingFeesForRetiredPersonnel.total + this.postList.retireePhoneBill.total + this.postList.otherSmallGauge.total + this.postList.meritPayTotal.total + this.postList.countrySetsAllowanceSubtotal.total + this.postList.subtotalOfBasicSalary.total;
        this.postList.totalAmount.financialAid = this.postList.retiredPersonnelSubsidyFee.financialAid + this.postList.wagesOfTemporaryWorkers.financialAid + this.postList.nursingFeesForRetiredPersonnel.financialAid + this.postList.retireePhoneBill.financialAid+ this.postList.otherSmallGauge.financialAid + this.postList.meritPayTotal.financialAid + this.postList.countrySetsAllowanceSubtotal.financialAid + this.postList.subtotalOfBasicSalary.financialAid;
        this.postList.totalAmount.otherAid = this.postList.retiredPersonnelSubsidyFee.otherAid + this.postList.wagesOfTemporaryWorkers.otherAid + this.postList.nursingFeesForRetiredPersonnel.otherAid + this.postList.retireePhoneBill.otherAid+ this.postList.otherSmallGauge.otherAid + this.postList.meritPayTotal.otherAid + this.postList.countrySetsAllowanceSubtotal.otherAid + this.postList.subtotalOfBasicSalary.otherAid;
      },
      addItem(){
        if(this.postList.otherDetailList.length>0){
          let num1 = this.postList.otherDetailList[this.postList.otherDetailList.length-1].number*this.postList.otherDetailList[this.postList.otherDetailList.length-1].price;
          let num2 = this.postList.otherDetailList[this.postList.otherDetailList.length-1].financialAid+this.postList.otherDetailList[this.postList.otherDetailList.length-1].otherAid;
          if(num1==num2){
            let obj = {};
            obj.number = 0;
            obj.price = 0;
            obj.financialAid = 0;
            obj.otherAid = 0;
            obj.total = 0;
            this.postList.otherDetailList.push(obj)
          }else {
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      deleteDetailItem(index){
        if(this.postList.otherDetailList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.otherDetailList.splice(index,1)
        }
      },
      getAllCheck(list){
        list.forEach((item ,index)=>{
          if((list[index].otherAid==0&&list[index].financialAid==0)||list[index].financialAid||list[index].otherAid){
            let num = list[index].number*list[index].price;
            let num2 = list[index].financialAid + list[index].otherAid;
            if(num!==num2){
               this.$Message.error({content:'第'+(index+1)+'行数量与单价之积需与财政补助收入与其他收入之和相等',duration:5});
            }
          }
        })
      },
      dataTrue(item){
        return (((item.number*item.price)==(item.financialAid + item.otherAid)))
      },
      handleOtherList(list){
        return list.every(this.dataTrue)
      },
      drawerCancel(){
        this.drawer = false;
        this.postList.otherDetailList = this.modifyObj;
      },
      drawerSave(){
        this.getAllCheck(this.postList.otherDetailList);
        if(this.handleOtherList(this.postList.otherDetailList)){
          let total = 0;
          let financialAid = 0;
          let otherAid = 0;
          this.postList.otherDetailList.forEach(item=>{
            total += item.total;
            financialAid += item.financialAid;
            otherAid += item.otherAid;
          })
          this.postList.other.total = total;
          this.postList.other.financialAid = financialAid;
          this.postList.other.otherAid = otherAid;
          this.getAllowanceTotal();
          this.getAmountTotal();
          this.drawer = false;
        }
      },
      tempDrawerCancel(){
        this.tempDrawer = false;
        this.postList.wagesOfTemporaryWorkersDetailList = this.modifyTempObj;
      },
      tempDrawerSave(){
        this.getAllCheck(this.postList.wagesOfTemporaryWorkersDetailList);
        if(this.handleOtherList(this.postList.wagesOfTemporaryWorkersDetailList)){
          let total = 0;
          let financialAid = 0;
          let otherAid = 0;
          this.postList.wagesOfTemporaryWorkersDetailList.forEach(item=>{
            total += item.total;
            financialAid += item.financialAid;
            otherAid += item.otherAid;
          });
          this.postList.wagesOfTemporaryWorkers.total = total;
          this.postList.wagesOfTemporaryWorkers.financialAid = financialAid;
          this.postList.wagesOfTemporaryWorkers.otherAid = otherAid;
          this.getAmountTotal();
          this.tempDrawer = false;
        }
      },
      modifyTemp(){
        this.modifyTempObj = JSON.parse(JSON.stringify(this.postList.wagesOfTemporaryWorkersDetailList));
        this.tempDrawer = true;
      },
      addTempItem(){
        if(this.postList.wagesOfTemporaryWorkersDetailList.length>0){
          let num1 = this.postList.wagesOfTemporaryWorkersDetailList[this.postList.wagesOfTemporaryWorkersDetailList.length-1].number*this.postList.wagesOfTemporaryWorkersDetailList[this.postList.wagesOfTemporaryWorkersDetailList.length-1].price;
          let num2 = this.postList.wagesOfTemporaryWorkersDetailList[this.postList.wagesOfTemporaryWorkersDetailList.length-1].financialAid+this.postList.wagesOfTemporaryWorkersDetailList[this.postList.wagesOfTemporaryWorkersDetailList.length-1].otherAid;
          if(num1==num2){
            let obj = {};
            obj.number = 0;
            obj.price = 0;
            obj.financialAid = 0;
            obj.otherAid = 0;
            obj.total = 0;
            this.postList.wagesOfTemporaryWorkersDetailList.push(obj)
          }else {
            this.$Message.error({content:'数量与单价之积需与财政补助收入与其他收入之和相等',duration:5})
          }
        }
      },
      deleteTempItem(index){
        if(this.postList.wagesOfTemporaryWorkersDetailList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.postList.wagesOfTemporaryWorkersDetailList.splice(index,1)
        }
      },
      sureSubmit(){
        this.postList.peopleId = this.$route.query.id;
        this.getAmountTotal();
        this.getOnJobTotal();
        this.$http.post('/api/budgetManage/saveBudgetFundsPeopleProjectDetail',this.postList).then(res=>{
          if(res.messageCode==10000){
            this.$Message.success(res.messageContent);
            this.$router.push({name:'funds-detail'});
          }else {
            this.$Message.error(res.messageContent);
          }
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
        top:-40px;
        left: 30px;
        cursor: pointer;
    }
    .view-icon{
        float: right;
        position: relative;
        top: 20px;
        left: 55px;
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