<template>
    <div class="love-students">
        <!--模块菜单-->
        <block-menu :blockMenuList="blockMenuList"></block-menu>
        <!--模块内容 block-container公共样式-->
        <div class="block-container">
            <router-view/>
        </div>
    </div>
</template>

<script>
  import BlockMenu from '../../components/BlockMenu.vue'
  export default {
    name: "LoveStudents",
    components:{
      BlockMenu
    },
    data(){
      return {
        blockMenuList: [
          {name: '非税收入执收及其他收入项目情况表', id: 1, pathName: 'budget-manage'},
          {name: '人员经费明细表(事业)', id: 2, pathName: 'funds-detail'},
          {name: '公用经费明细表(行政、事业)', id: 3, pathName: 'non-personnel-funds'},
          {name: '项目支出情况预算表', id: 4, pathName: 'project-expenditure'}
        ]
      }
    },
    created(){
      this.getSecondMenuList()
    },
    methods:{
      getSecondMenuList(){
        this.$http.get('/api/roleSelect/getChildResources?parentId='+this.$route.query.id).then(res=>{
          this.blockMenuList = res.result.resources;
        })
      }
    }
  }
</script>