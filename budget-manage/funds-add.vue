<template>
    <div class="donation-manage">
        <!--面包屑导航-->
        <div class="top">
            <Breadcrumb>
                <BreadcrumbItem><img class="crumb-icon" src="../../assets/place.png" alt="place">预算管理</BreadcrumbItem>
                <BreadcrumbItem to="/home/budget-manage/funds-detail">人员经费明细表(事业)</BreadcrumbItem>
                <BreadcrumbItem>新建档案</BreadcrumbItem>
            </Breadcrumb>
            <router-link :to="{ name: 'funds-detail'}"><div class="go-back">返回</div></router-link>
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
            <Col class="com-key" span="8">项目</Col>
            <Col class="com-key" span="4">总计(元)</Col>
            <Col class="com-key" span="4">财政补助收入（元）</Col>
            <Col class="com-key" span="4">其他收入（元）</Col>
            <Col class="com-key" span="4">备注</Col>
            <Col class="com-value" span="8">在职人员经费总计</Col>
            <Col class="com-value" span="4">
                <span>{{onJob.total}}</span>
                <!--<InputNumber  class="value-input" :min="0" :max="999999999"  v-model="onJob.total"></InputNumber>-->
            </Col>
            <Col class="com-value" span="4">
                <span>{{onJob.financialAid}}</span>
                <!--<InputNumber  class="value-input" :min="0" :max="999999999" v-model="onJob.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="4">
                <span>{{onJob.otherAid}}</span>
                <!--<InputNumber  class="value-input" :min="0" :max="999999999" v-model="onJob.financialAid"></InputNumber>-->
            </Col>
            <Col class="com-value" span="4">
                <span>{{onJob.remarks}}</span>
                <!--<Input type="textarea" :maxlength="200" class="value-input" v-model="onJob.remarks"></Input>-->
            </Col>
            <Col class="com-value" span="8">岗位工资</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0"
                              :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postSalary.total" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postSalary.financialAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="postSalary.otherAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="postSalary.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">薪级工资</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="salaryRank.total" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="salaryRank.financialAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="salaryRank.otherAid" @on-blur="getSalaryTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="salaryRank.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">基本工资小计</Col>
            <Col class="com-value" span="4">
                <span>{{subtotalOfBasicSalary.total}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="subtotalOfBasicSalary.financialAid"></InputNumber>-->
                <span>{{subtotalOfBasicSalary.financialAid}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<InputNumber  class="value-input" :min="0" v-model="subtotalOfBasicSalary.financialAid"></InputNumber>-->
                <span>{{subtotalOfBasicSalary.otherAid}}</span>
            </Col>
            <Col class="com-value" span="4">
                <!--<Input type="textarea" class="value-input" v-model="subtotalOfBasicSalary.remarks"></Input>-->
                <span>{{subtotalOfBasicSalary.remarks}}</span>
            </Col>
            <Col class="com-value" span="8">上下班交通费补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="commutingAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="commutingAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="commutingAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="commutingAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">独生子女父母奖励费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="incentiveFeesForParentsOfOnlyChildren.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="incentiveFeesForParentsOfOnlyChildren.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="incentiveFeesForParentsOfOnlyChildren.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="incentiveFeesForParentsOfOnlyChildren.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">粮油补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="grainAndOilSubsidies.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="grainAndOilSubsidies.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="grainAndOilSubsidies.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="grainAndOilSubsidies.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">教龄津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="schoolAgeAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input"
                              :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="schoolAgeAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="schoolAgeAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="schoolAgeAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">护龄津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="protectTheAgeAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="protectTheAgeAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="protectTheAgeAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="protectTheAgeAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">政府特殊津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="governmentSpecialAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="governmentSpecialAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="governmentSpecialAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="governmentSpecialAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">各类特殊岗位津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="allKindsOfSpecialPostAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="allKindsOfSpecialPostAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="allKindsOfSpecialPostAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="allKindsOfSpecialPostAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">选派青年志愿人员赴云南扶贫补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="yunnan.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="yunnan.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="yunnan.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="yunnan.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">选派干部赴西藏等省市补贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="tibet.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="tibet.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="tibet.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="tibet.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">特级教师津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="specialTeacherAllowance.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="specialTeacherAllowance.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="specialTeacherAllowance.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="specialTeacherAllowance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">支教人员津贴</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="allowanceForVolunteerTeachers.total" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="allowanceForVolunteerTeachers.financialAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="allowanceForVolunteerTeachers.otherAid" @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="allowanceForVolunteerTeachers.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">其他</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="other.total" readonly @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="other.financialAid" readonly @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="other.otherAid" readonly @on-blur="getAllowanceTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input"  v-model="other.remarks"  style="position: relative;left: 17px"></Input>
                <img src="../../assets/icon/view-icon.png" @click="viewDrawer = true" alt="" class="view-icon">
                <img src="../../assets/icon/modify-icon.png" @click="modifyOther" alt="" class="add-icon">
            </Col>
            <Col class="com-total" span="8">国家规定津补贴小计</Col>
            <Col class="com-total" span="4">
                <span>{{countrySetsAllowanceSubtotal.total}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{countrySetsAllowanceSubtotal.financialAid}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{countrySetsAllowanceSubtotal.otherAid}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{countrySetsAllowanceSubtotal.remarks}}</span>
            </Col>
            <Col class="com-value" span="8">绩效工资（一）</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="meritPayOne.total" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="meritPayOne.financialAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="meritPayOne.otherAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="meritPayOne.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">绩效工资（二）：高层次人才倾斜</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="meritPayTwo.total" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="meritPayTwo.financialAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="meritPayTwo.otherAid" @on-blur="getMeritPayTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="meritPayTwo.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">绩效工资小计</Col>
            <Col class="com-total" span="4">
                <span>{{meritPayTotal.total}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{meritPayTotal.financialAid}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{meritPayTotal.otherAid}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{meritPayTotal.remarks}}</span>
            </Col>
            <Col class="com-value" span="8"> 职工养老保险16%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="employeePensionInsurance.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="employeePensionInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="employeePensionInsurance.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="employeePensionInsurance.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">公积金7%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="accumulationFund.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="accumulationFund.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="accumulationFund.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="accumulationFund.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 失业保险费0.5%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="unemploymentInsurance.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="unemploymentInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="unemploymentInsurance.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="unemploymentInsurance.remarks"></Input>
            </Col>
            <!--<Col class="com-value" span="8">生育保险费1%</Col>-->
            <!--<Col class="com-value" span="4">-->
                <!--<InputNumber  class="value-input" :min="0" :max="999999999" v-model="maternityInsurance.total" @on-blur="getOtherTotal"></InputNumber>-->
            <!--</Col>-->
            <!--<Col class="com-value" span="4">-->
                <!--<InputNumber  class="value-input" :min="0" :max="999999999" v-model="maternityInsurance.financialAid" @on-blur="getOtherTotal"></InputNumber>-->
            <!--</Col>-->
            <!--<Col class="com-value" span="8">-->
                <!--<Input type="textarea" :maxlength="200" class="value-input" v-model="maternityInsurance.remarks"></Input>-->
            <!--</Col>-->
            <Col class="com-value" span="8"> 工伤保险费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="injuryInsurancePremium.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="injuryInsurancePremium.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="injuryInsurancePremium.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="injuryInsurancePremium.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 医疗保险费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="medicalInsurancePremium.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="medicalInsurancePremium.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="medicalInsurancePremium.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="medicalInsurancePremium.remarks"></Input>
            </Col>
            <Col class="com-value" span="8">  职业年金 8%</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="occupationalPension.total" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="occupationalPension.financialAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="occupationalPension.otherAid" @on-blur="getOtherTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="occupationalPension.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">其他小计</Col>
            <Col class="com-total" span="4">
                <span>{{otherSmallGauge.total}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{otherSmallGauge.financialAid}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{otherSmallGauge.otherAid}}</span>
            </Col>
            <Col class="com-total" span="4">
                <span>{{otherSmallGauge.remarks}}</span>
            </Col>
            <Col class="com-value" span="8"> 临时工工资：经费（4800元/人）</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="wagesOfTemporaryWorkers.total" readonly @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="wagesOfTemporaryWorkers.financialAid" readonly @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="wagesOfTemporaryWorkers.otherAid" readonly @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="wagesOfTemporaryWorkers.remarks"  style="position:relative;left: 15px"></Input>
                <img src="../../assets/icon/view-icon.png" @click="tempViewDrawer = true" alt="" class="view-icon">
                <img src="../../assets/icon/modify-icon.png" @click="modifyTemp" alt="" class="add-icon">
            </Col>
            <Col class="com-value" span="8"> 事业单位离休人员补贴费</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="retiredPersonnelSubsidyFee.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="retiredPersonnelSubsidyFee.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="retiredPersonnelSubsidyFee.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="retiredPersonnelSubsidyFee.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 离休人员护工费、护理费、电话费等</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="nursingFeesForRetiredPersonnel.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="nursingFeesForRetiredPersonnel.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="nursingFeesForRetiredPersonnel.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="nursingFeesForRetiredPersonnel.remarks"></Input>
            </Col>
            <Col class="com-value" span="8"> 退休人员电话费等</Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              readonly
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="retireePhoneBill.total" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="retireePhoneBill.financialAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <InputNumber  class="value-input" :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                              v-model="retireePhoneBill.otherAid" @on-blur="getAmountTotal"></InputNumber>
            </Col>
            <Col class="com-value" span="4">
                <Input type="textarea" :maxlength="200" class="value-input" v-model="retireePhoneBill.remarks"></Input>
            </Col>
            <Col class="com-total" span="8">总合计</Col>
            <Col class="com-value" span="4">
                <span>{{totalAmount.total}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{totalAmount.financialAid}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{totalAmount.otherAid}}</span>
            </Col>
            <Col class="com-value" span="4">
                <span>{{totalAmount.remarks}}</span>
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
                <div v-for="(item,index) in otherDetailList">
                    <Col class="com-value" span="4"><InputNumber :min="0" :max="999999999"
                                                                 :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                                                 :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                                                 v-model="item.number" class="value-input" @on-blur="getTotal(index)" @on-change="getChangeTotal($event,index)"  ></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber    :min="0" :max="999999999"
                                        :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                        :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                        v-model="item.price" class="value-input" @on-blur="getTotal(index)" @on-change="getChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber
                                :min="0" :max="999999999"
                                :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                v-model="item.financialAid" class="value-input">

                        </InputNumber>
                    </Col>
                    <Col class="com-value" span="5">
                        <InputNumber    :min="0" :max="999999999"
                              :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                              :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                        v-model="item.otherAid" class="value-input">
                        </InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" :max="999999999" v-model="item.total" readonly class="value-input"></InputNumber>
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
                <div v-for="(item,index) in wagesOfTemporaryWorkersDetailList">
                    <Col class="com-value" span="4">
                        <InputNumber :min="0" :max="999999999"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     v-model="item.number" class="value-input" @on-blur="getTempTotal(index)" @on-change="getTempChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" :max="999999999"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     v-model="item.price" class="value-input" @on-blur="getTempTotal(index)" @on-change="getTempChangeTotal($event,index)"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" :max="999999999"
                                     :formatter="value => ` ${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')"
                                     :parser="value => value.replace(/\$\s?|(,*)/g, '')"
                                     v-model="item.financialAid" class="value-input"></InputNumber></Col>
                    <Col class="com-value" span="5">
                        <InputNumber :min="0" :max="999999999"
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
                <div v-for="(item,index) in otherDetailList">
                    <Col class="com-value" span="4"><span>{{item.number}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.price}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.financialAid}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.otherAid}}</span></Col>
                    <Col class="com-value" span="5">
                        <span>{{item.total}}</span>
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
                <div v-for="(item,index) in wagesOfTemporaryWorkersDetailList">
                    <Col class="com-value" span="4"><span>{{item.number}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.price}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.financialAid}}</span></Col>
                    <Col class="com-value" span="5"><span>{{item.otherAid}}</span></Col>
                    <Col class="com-value" span="5">
                        <span>{{item.total}}</span>
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
        drawer:false,
        viewDrawer:false,
        tempDrawer:false,
        tempViewDrawer:false,
        peopleId:'',
        modifyObj:'',//copy取消对象
        modifyTempObj:'',//copy取消对象
        otherListCheck:true,
        tempListCheck:true,
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
          otherAid:0,
          remarks:"/"
        },
        postSalary:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        salaryRank:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        subtotalOfBasicSalary:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:"/"
        },

        //国家规定津补贴
        commutingAllowance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        incentiveFeesForParentsOfOnlyChildren:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        grainAndOilSubsidies:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        schoolAgeAllowance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        protectTheAgeAllowance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        governmentSpecialAllowance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        allKindsOfSpecialPostAllowance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        yunnan:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        tibet:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        specialTeacherAllowance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        allowanceForVolunteerTeachers:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        other:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        otherDetailList:[
          {total:null,price:null,financialAid:null,otherAid:null,number:null}
        ],
        countrySetsAllowanceSubtotal:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:"/"
        },

        //绩效工资
        meritPayOne:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        meritPayTwo:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        meritPayTotal:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:"/"
        },

        //其他小计
        employeePensionInsurance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        accumulationFund:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        unemploymentInsurance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        maternityInsurance:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        injuryInsurancePremium:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        medicalInsurancePremium:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        occupationalPension:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        otherSmallGauge:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:"/"
        },

        //总合计
        retiredPersonnelSubsidyFee:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        wagesOfTemporaryWorkers:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        wagesOfTemporaryWorkersDetailList:[
          {
            "number": null,//数量
            "price": null,//单价
            "financialAid": null,//财政补助收入
            "otherAid": null,//其他收入
            "total": null//总价
          },
        ],
        nursingFeesForRetiredPersonnel:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        retireePhoneBill:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:""
        },
        totalAmount:{
          total:null,
          financialAid:null,
          otherAid:null,
          remarks:"/"
        },


        tempList:[
          {totalNumber:1564,price:15,finance:5000,otherIncome:654,total:5654}
        ]
      }
    },
    mounted(){

    },
    methods: {
      modifyOther(){
        this.modifyObj = JSON.parse(JSON.stringify(this.otherDetailList));
        this.drawer = true;
      },
      getTotal(index){
        // this.getCheck(index)
        if(this.otherDetailList[index].price&&this.otherDetailList[index].number){
          this.otherDetailList[index].total = this.otherDetailList[index].number*this.otherDetailList[index].price;
        }
      },
      getChangeTotal(event,index){
        if(this.otherDetailList[index].price&&this.otherDetailList[index].number){
          this.otherDetailList[index].total = this.otherDetailList[index].number*this.otherDetailList[index].price;
        }
      },
      getCheck(index){
        if(this.otherDetailList[index].financialAid&&this.otherDetailList[index].otherAid){
          let num = this.otherDetailList[index].number*this.otherDetailList[index].price;
          let num2 = this.otherDetailList[index].financialAid + this.otherDetailList[index].otherAid;
          if(num!==num2){
            this.$Message.error('数量与单价之积需与财政补助收入与其他收入之和相等',5);
            return false
          }
        }
      },
      getTempChangeTotal(event,index){
        this.getTempCheck(index);
        if(this.wagesOfTemporaryWorkersDetailList[index].price&&this.wagesOfTemporaryWorkersDetailList[index].number){
          this.wagesOfTemporaryWorkersDetailList[index].total = this.wagesOfTemporaryWorkersDetailList[index].number*this.wagesOfTemporaryWorkersDetailList[index].price;
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
            this.$Message.error('数量与单价之积需与财政补助收入与其他收入之和相等',5)
          }
        }
      },
      getSalaryTotal(){
        this.postSalary.total = this.postSalary.financialAid + this.postSalary.otherAid;
        this.salaryRank.total = this.salaryRank.financialAid + this.salaryRank.otherAid;
        this.subtotalOfBasicSalary.total = this.postSalary.total + this.salaryRank.total;
        this.subtotalOfBasicSalary.financialAid = this.postSalary.financialAid + this.salaryRank.financialAid;
        this.subtotalOfBasicSalary.otherAid = this.postSalary.otherAid + this.salaryRank.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getAllowanceTotal(){
        //国家津贴各项总计计算
        this.commutingAllowance.total = this.commutingAllowance.financialAid + this.commutingAllowance.otherAid;
        this.incentiveFeesForParentsOfOnlyChildren.total = this.incentiveFeesForParentsOfOnlyChildren.financialAid + this.incentiveFeesForParentsOfOnlyChildren.otherAid;
        this.grainAndOilSubsidies.total = this.grainAndOilSubsidies.financialAid + this.grainAndOilSubsidies.otherAid;
        this.schoolAgeAllowance.total = this.schoolAgeAllowance.financialAid + this.schoolAgeAllowance.otherAid;
        this.protectTheAgeAllowance.total = this.protectTheAgeAllowance.financialAid + this.protectTheAgeAllowance.otherAid;
        this.governmentSpecialAllowance.total = this.governmentSpecialAllowance.financialAid + this.governmentSpecialAllowance.otherAid;
        this.allKindsOfSpecialPostAllowance.total = this.allKindsOfSpecialPostAllowance.financialAid + this.allKindsOfSpecialPostAllowance.otherAid;
        this.yunnan.total = this.yunnan.financialAid + this.yunnan.otherAid;
        this.tibet.total = this.tibet.financialAid + this.tibet.otherAid;
        this.specialTeacherAllowance.total = this.specialTeacherAllowance.financialAid + this.specialTeacherAllowance.otherAid;
        this.allowanceForVolunteerTeachers.total = this.allowanceForVolunteerTeachers.financialAid + this.allowanceForVolunteerTeachers.otherAid;
        this.other.total = this.other.financialAid + this.other.otherAid;
        //国家津贴小计
        this.countrySetsAllowanceSubtotal.total = this.commutingAllowance.total +this.incentiveFeesForParentsOfOnlyChildren.total +this.grainAndOilSubsidies.total +
          this.schoolAgeAllowance.total +this.protectTheAgeAllowance.total + this.governmentSpecialAllowance.total + this.allKindsOfSpecialPostAllowance.total +
          this.yunnan.total + this.tibet.total + this.specialTeacherAllowance.total + this.allowanceForVolunteerTeachers.total + this.other.total;
        this.countrySetsAllowanceSubtotal.financialAid = this.commutingAllowance.financialAid +this.incentiveFeesForParentsOfOnlyChildren.financialAid +this.grainAndOilSubsidies.financialAid +
          this.schoolAgeAllowance.financialAid +this.protectTheAgeAllowance.financialAid + this.governmentSpecialAllowance.financialAid + this.allKindsOfSpecialPostAllowance.financialAid +
          this.yunnan.financialAid + this.tibet.financialAid + this.specialTeacherAllowance.financialAid + this.allowanceForVolunteerTeachers.financialAid + this.other.financialAid;
        this.countrySetsAllowanceSubtotal.otherAid = this.commutingAllowance.otherAid +this.incentiveFeesForParentsOfOnlyChildren.otherAid +this.grainAndOilSubsidies.otherAid +
          this.schoolAgeAllowance.otherAid +this.protectTheAgeAllowance.otherAid + this.governmentSpecialAllowance.otherAid + this.allKindsOfSpecialPostAllowance.otherAid +
          this.yunnan.otherAid + this.tibet.otherAid + this.specialTeacherAllowance.otherAid + this.allowanceForVolunteerTeachers.otherAid + this.other.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getMeritPayTotal(){
        //绩效工资小计各项计算
        this.meritPayOne.total = this.meritPayOne.financialAid + this.meritPayOne.otherAid;
        this.meritPayTwo.total = this.meritPayTwo.financialAid + this.meritPayTwo.otherAid;
        //绩效工资小计
        this.meritPayTotal.total = this.meritPayOne.total + this.meritPayTwo.total;
        this.meritPayTotal.financialAid = this.meritPayOne.financialAid + this.meritPayTwo.financialAid;
        this.meritPayTotal.otherAid = this.meritPayOne.otherAid + this.meritPayTwo.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getOtherTotal(){
        //其他小计各项计算
        this.employeePensionInsurance.total = this.employeePensionInsurance.financialAid + this.employeePensionInsurance.otherAid;
        this.accumulationFund.total = this.accumulationFund.financialAid + this.accumulationFund.otherAid;
        this.unemploymentInsurance.total = this.unemploymentInsurance.financialAid + this.unemploymentInsurance.otherAid;
        this.maternityInsurance.total = this.maternityInsurance.financialAid + this.maternityInsurance.otherAid;
        this.injuryInsurancePremium.total = this.injuryInsurancePremium.financialAid + this.injuryInsurancePremium.otherAid;
        this.medicalInsurancePremium.total = this.medicalInsurancePremium.financialAid + this.medicalInsurancePremium.otherAid;
        this.occupationalPension.total = this.occupationalPension.financialAid + this.occupationalPension.otherAid;
        //其他小计
        this.otherSmallGauge.total = this.employeePensionInsurance.total + this.accumulationFund.total + this.unemploymentInsurance.total + this.maternityInsurance.total+
          this.injuryInsurancePremium.total + this.medicalInsurancePremium.total + this.occupationalPension.total;
        this.otherSmallGauge.financialAid = this.employeePensionInsurance.financialAid + this.accumulationFund.financialAid + this.unemploymentInsurance.financialAid + this.maternityInsurance.financialAid+
          this.injuryInsurancePremium.financialAid + this.medicalInsurancePremium.financialAid + this.occupationalPension.financialAid;
        this.otherSmallGauge.otherAid = this.employeePensionInsurance.otherAid + this.accumulationFund.otherAid + this.unemploymentInsurance.otherAid + this.maternityInsurance.otherAid+
          this.injuryInsurancePremium.otherAid + this.medicalInsurancePremium.otherAid + this.occupationalPension.otherAid;
        this.getOnJobTotal();
        this.getAmountTotal();
      },
      getOnJobTotal(){
        this.onJob.total =  this.otherSmallGauge.total + this.meritPayTotal.total + this.countrySetsAllowanceSubtotal.total + this.subtotalOfBasicSalary.total;
        this.onJob.financialAid = this.otherSmallGauge.financialAid + this.meritPayTotal.financialAid + this.countrySetsAllowanceSubtotal.financialAid + this.subtotalOfBasicSalary.financialAid;
        this.onJob.otherAid = this.otherSmallGauge.otherAid + this.meritPayTotal.otherAid + this.countrySetsAllowanceSubtotal.otherAid + this.subtotalOfBasicSalary.otherAid;
      },
      getAmountTotal(){
        //总合计各项小计
        this.retiredPersonnelSubsidyFee.total = this.retiredPersonnelSubsidyFee.financialAid + this.retiredPersonnelSubsidyFee.otherAid;
        this.wagesOfTemporaryWorkers.total = this.wagesOfTemporaryWorkers.financialAid + this.wagesOfTemporaryWorkers.otherAid;
        this.nursingFeesForRetiredPersonnel.total = this.nursingFeesForRetiredPersonnel.financialAid + this.nursingFeesForRetiredPersonnel.otherAid;
        this.retireePhoneBill.total = this.retireePhoneBill.financialAid + this.retireePhoneBill.otherAid;
        //总合计
        this.totalAmount.total = this.retiredPersonnelSubsidyFee.total + this.wagesOfTemporaryWorkers.total + this.nursingFeesForRetiredPersonnel.total + this.retireePhoneBill.total + this.otherSmallGauge.total + this.meritPayTotal.total + this.countrySetsAllowanceSubtotal.total + this.subtotalOfBasicSalary.total;
        this.totalAmount.financialAid = this.retiredPersonnelSubsidyFee.financialAid + this.wagesOfTemporaryWorkers.financialAid + this.nursingFeesForRetiredPersonnel.financialAid + this.retireePhoneBill.financialAid + this.otherSmallGauge.financialAid + this.meritPayTotal.financialAid + this.countrySetsAllowanceSubtotal.financialAid + this.subtotalOfBasicSalary.financialAid;
        this.totalAmount.otherAid = this.retiredPersonnelSubsidyFee.otherAid + this.wagesOfTemporaryWorkers.otherAid + this.nursingFeesForRetiredPersonnel.otherAid + this.retireePhoneBill.otherAid + this.otherSmallGauge.otherAid + this.meritPayTotal.otherAid + this.countrySetsAllowanceSubtotal.otherAid + this.subtotalOfBasicSalary.otherAid;
      },
      addItem(){
        let obj = {};
        obj.number = null;
        obj.price = null;
        obj.financialAid = null;
        obj.otherAid = null;
        obj.total = null;
        this.otherDetailList.push(obj)
      },
      deleteDetailItem(index){
        if(this.otherDetailList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.otherDetailList.splice(index,1)
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
        this.otherDetailList = this.modifyObj;
      },
      drawerSave(){
        this.getAllCheck(this.otherDetailList);
        if(this.handleOtherList(this.otherDetailList)){
          let total = 0;
          let financialAid = 0;
          let otherAid = 0;
          this.otherDetailList.forEach(item=>{
            total += item.total;
            financialAid += item.financialAid;
            otherAid += item.otherAid;
          })
          this.other.total = total;
          this.other.financialAid = financialAid;
          this.other.otherAid = otherAid;
          this.getAllowanceTotal();
          this.getAmountTotal();
          this.drawer = false;
        }
      },
      tempDrawerCancel(){
        this.tempDrawer = false;
        this.wagesOfTemporaryWorkersDetailList = this.modifyTempObj;
      },
      tempDrawerSave(){
        this.getAllCheck(this.wagesOfTemporaryWorkersDetailList);
        if(this.handleOtherList(this.wagesOfTemporaryWorkersDetailList)){
          let total = 0;
          let financialAid = 0;
          let otherAid = 0;
          this.wagesOfTemporaryWorkersDetailList.forEach(item=>{
            total += item.total;
            financialAid += item.financialAid;
            otherAid += item.otherAid;
          });
          this.wagesOfTemporaryWorkers.total = total;
          this.wagesOfTemporaryWorkers.financialAid = financialAid;
          this.wagesOfTemporaryWorkers.otherAid = otherAid;
          this.getAmountTotal();
          this.tempDrawer = false;
        }
      },
      modifyTemp(){
        this.modifyTempObj = JSON.parse(JSON.stringify(this.wagesOfTemporaryWorkersDetailList));
        this.tempDrawer = true;
      },
      addTempItem(){
        let obj = {};
        obj.number = null;
        obj.price = null;
        obj.financialAid = null;
        obj.otherAid = null;
        obj.total = null;
        this.wagesOfTemporaryWorkersDetailList.push(obj)
      },
      deleteTempItem(index){
        if(this.wagesOfTemporaryWorkersDetailList.length==1){
          this.$Message.error({content:'请至少保留一项明细',duration:5})
        }else {
          this.wagesOfTemporaryWorkersDetailList.splice(index,1)
        }
      },
      sureSubmit(){
        if(!this.year){
         this.$Message.error({content:'请填写预算年度',duration:5})
        }else {
          this.$http.get('/api/budgetManage/saveBudgetFundsPeople?year='+this.year).then(res=>{
            if(res.messageCode==10000){
              this.peopleId = res.result.id;
              this.getAmountTotal();
              this.getOnJobTotal();
              let param = {
                "peopleId":this.peopleId,
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
              };
              this.$http.post('/api/budgetManage/saveBudgetFundsPeopleProjectDetail',param).then(res=>{
                if(res.messageCode==10000){
                  this.$Message.success(res.messageContent);
                  this.$router.push({name:'funds-detail'});
                }else {
                  this.$Message.error(res.messageContent);
                }
              })
            }else {
              this.$Message.info(res.messageContent)
            }
          })
        }
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