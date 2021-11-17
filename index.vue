<template>
  <basic-container>
      <p class="hot_title">指定权限设置</p>
    <div>
      <avue-crud
        ref="crud"
        class="batch-choose"
        :data="tableData"
        :option="listOption"
        :page.sync="page"
        @on-load="getAppoint"
        @size-change="sizeChange"
        @current-change="currentChange"
      >
        <template slot="name" slot-scope="scope">
          <span v-if="scope.row.id != 6 && scope.row.id != 8">{{ scope.row.name }}</span>
          <div v-else>
              <div v-if="scope.row.permissionEngineer && scope.row.id == 6">
                <span>默认工程师：</span>
                <span v-if="scope.row.permissionEngineer.defaultPatentEngineerName">专利：{{ scope.row.permissionEngineer.defaultPatentEngineerName }}</span>
                <span v-if="scope.row.permissionEngineer.defaultTrademarkEngineerName">商标：{{ scope.row.permissionEngineer.defaultTrademarkEngineerName }}</span>
                <span v-if="scope.row.permissionEngineer.defaultCopyrightEngineerName">版权：{{ scope.row.permissionEngineer.defaultCopyrightEngineerName }}</span>
                <span v-if="scope.row.permissionEngineer.defaultOtherEngineerName">其他：{{ scope.row.permissionEngineer.defaultOtherEngineerName }}</span>
              </div>
              <div v-if="scope.row.id == 8">默认工程师：{{ scope.row.defaultName }}</div>
              <div>可选工程师：<span>{{ scope.row.name }}</span></div>                    
          </div>
          
        </template>
        <template slot="menu" slot-scope="scope">
          <el-button type="text" icon="el-icon-view" @click="handldEdit(scope.row)">编辑</el-button>
        </template>        
      </avue-crud>
       <el-dialog title="编辑指定权限" v-if="centerDialogVisible" :close-on-click-modal="false"  :visible.sync="centerDialogVisible" width="680px" center>
           <el-form  :model="appointForm" :rules="rules" ref="appointForm">
                 <el-form-item label="权限名称：">
                     <span>{{appointForm.permissionName}}</span>
                </el-form-item>
                <el-form-item label="权限人：" prop="radio" v-if="appointForm.id != 6 && appointForm.id != 8">
                  <span v-if="appointForm.id == 1 || appointForm.id == 2 || appointForm.id == 3 || appointForm.id == 4" style="margin-right: 20px">
                    <el-radio v-model="radio" label="1" v-if="notShow==true">不限</el-radio>
                    <el-radio v-model="radio" label="2">自定义</el-radio>
                  </span>
                    <template v-if="radio== 2 ||  appointForm.id == 9 ">
                        <el-cascader
                            ref="cascater"
                            :key="refreshKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="companyList"
                            v-model="appointPerson"
                            @change="handldeChange"
                            @remove-tag="removeTag"
                            :props="{ value: 'customerId', label: 'label',multiple: true }"
                        />
                        <span class="parallel" v-if="appointForm.id != 1 && appointForm.id != 2 && appointForm.id != 3 && appointForm.id != 4">可多选,最多10人，已选择{{this.appointPerson.length}}人</span>
                    </template>
                </el-form-item>
                <el-form-item label="默认工程师：" prop="defaultEngineer" v-if="appointForm.id == 6 || appointForm.id == 8 ">
                    <div v-if="appointForm.id == 8">
                        <el-cascader
                            ref="cascater"
                            :key="defaultKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="companyList"
                            v-model="defaultEngineer"
                            @change="handldeChange"
                            
                            :props="{ value: 'customerId', label: 'label',multiple: true }"
                        />
                        <span class="parallel">可多选，最多10人，已选择{{this.defaultEngineer.length}}人</span>
                    </div>                                  
                </el-form-item> 
                <div v-if="appointForm.id == 6" style="margin-left:6px">
                      <el-form-item label="专利工程师：">
                        <el-cascader
                            ref="cascater"
                            :key="patentKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="companyList"
                            v-model="patentEngineer"
                            @visible-change="removePatent($event,patentEngineer)"
                            @change="handldeChange"
                            :props="{ value: 'customerId', label: 'label',multiple: true }"
                        />
                        <span class="parallel">可多选，最多10人，已选择{{this.patentEngineer.length}}人</span>
                      </el-form-item>
                      <el-form-item label="商标工程师：">
                        <el-cascader
                            ref="cascater"
                            :key="brandKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="companyList"
                            v-model="brandEngineer"
                            @visible-change="removeBrand($event,brandEngineer)"
                            @change="handldeChange"
                            :props="{ value: 'customerId', label: 'label',multiple: true }"
                        />
                        <span class="parallel">可多选，最多10人，已选择{{this.brandEngineer.length}}人</span>
                      </el-form-item>
                      <el-form-item label="版权工程师：">
                        <el-cascader
                            ref="cascater"
                            :key="copyrightKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="companyList"
                            v-model="copyrightEngineer"
                            @visible-change="removeCopyright($event,copyrightEngineer)"
                            @change="handldeChange"
                            :props="{ value: 'customerId', label: 'label',multiple: true }"
                        />
                        <span class="parallel">可多选，最多10人，已选择{{this.copyrightEngineer.length}}人</span>
                      </el-form-item>
                      <el-form-item label="其他工程师：">
                        <el-cascader
                            ref="cascater"
                            :key="otherKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="companyList"
                            v-model="otherEngineer"
                            @visible-change="removeOther($event,otherEngineer)"
                            @change="handldeChange"
                            :props="{ value: 'customerId', label: 'label',multiple: true }"
                        />
                        <span class="parallel">可多选，最多10人，已选择{{this.otherEngineer.length}}人</span>
                      </el-form-item>
                    </div>                       
                <el-form-item label="可选工程师：" prop="selectiveEngineer" v-if="appointForm.id == 6 || appointForm.id == 8 ">
                    <template>
                        <el-cascader
                            ref="cascater"
                            :key="selectKey"
                            clearable
                            filterable
                            collapse-tags
                            style="width: 250px;"
                            :show-all-levels="false"
                            :options="selectList"
                            v-model="selectiveEngineer"
                            @change="handldeChange"
                            @remove-tag="removeTag"
                            :props="{ value: 'customerId', label: 'label', multiple: true,}"
                        />
                        <span class="parallel">可多选，最多50人，已选择{{this.selectiveEngineer.length}}人</span>
                    </template>
                </el-form-item>
                  <div v-if="radio==2 && appointForm.id != 5 && appointForm.id != 6 && appointForm.id != 7 && appointForm.id != 8 && appointForm.id != 9" :class="[notShow==false?'teshu':'','tip']">可多选,最多10人，已选择{{this.appointPerson.length}}人</div>
                  <div style="margin-top:30px">说明：指定权限人前，请先配置其菜单权限，确保其可使用相应菜单。</div>
           </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button v-if="appointForm.id==6" type="primary" @click="handleProperty">确 定</el-button>
                <el-button v-else type="primary" @click="handleUpdata">确 定</el-button>
                <el-button @click="handleCancle">取 消</el-button>
           </span>
        </el-dialog>
    </div>
  </basic-container>
</template>

<script>
import { getList,editAppoint } from "@/api/admin/appoint";
import { getEmpList } from "@/api/clue/clue";
import { listOption } from "@/const/crud/admin/appoint";

export default {
  data() {
    return {
      radio:'1',
      notShow:true,
      refreshKey:0,
      defaultKey:0,
      selectKey:0,
      recordList:[],
      companyList:[],
      selectList:[],
      appointPerson:[],   // 权限人
      defaultEngineer:[],
      patentEngineer:[],
      brandEngineer:[],
      copyrightEngineer:[],
      otherEngineer:[],
      selectiveEngineer:[],
      centerDialogVisible:false,
      params:{},
      page: {
        currentPage: 1,
        total: 0,
        layout: "total, sizes, prev, pager, next, jumper",
        background: true,
        pageSizes: [5, 8, 10, 20, 30, 40, 50, 100], //选择每页显示条数
        pageSize: 20,
      },
      listOption: listOption,
      tableData: [],
      appointForm:{},
      rules:{
        radio: [
          { required: true, message: '', trigger: 'blur' },
        ],
        defaultEngineer:[
          { required: true, message: '', trigger: 'blur' },
        ],
        selectiveEngineer:[
          { required: true, message: '', trigger: 'blur' },
        ],          
      },
    };
  },
  mounted() {
    this.getData();
  },
    watch:{
        'appointPerson':{
            handler(newVal, oldVal){
                console.log(this.appointPerson,'appointPerson');
                if(newVal.length == 11){
                    this.appointPerson = oldVal;
                    --this.refreshKey;
                    this.$message({
                        message: '最多只能选择10人！',
                        duration: 2000,
                        type: 'warning'
                    })
                }else if(newVal.length>11){
                    this.$message({
                        message: '最多只能选择10人！',
                        duration: 2000,
                        type: 'warning'
                    })
                    this.appointPerson = [];
                    newVal.slice(0,10).forEach(item => {
                        this.appointPerson.push(item);
                        ++this.refreshKey;
                    });
                }
            },
            deep: true,
            immediate: true
        },
        'defaultEngineer':{
            handler(newVal, oldVal){
              console.log(newVal,"ssssssssssssssssssssssssssssssssssss")
                ++this.defaultKey;
                if (newVal.length > 10) {
                this.$message({
                  message: '最多只能选择10项',
                  duration: 1500,
                  type: 'warning'
                })}else{
                   this.defaultEngineer = [];
                   newVal.forEach(item => {
                     this.defaultEngineer.push(item)
                   })
                   this.removeDefault(false)
                }
              // if (newVal.length > 10) {
              //   this.$message({
              //     message: '最多只能选择10项',
              //     duration: 1500,
              //     type: 'warning'
              //   })
              //   }else{
              //     console.log('3')
              //   this.$nextTick(() => {
              //     this.defaultEngineer = [];
              //     newVal.slice(0,10).forEach(item => {
              //         this.defaultEngineer.push(item);
              //         ++this.defaultKey;
              //     });
              //     this.removeDefault(false)
              //   })
              //   }
            },            
            deep: true,
            immediate: true
        },
        'patentEngineer':{
            handler(newVal, oldVal){
              if (newVal.length > 10) {
                this.$message({
                  message: '最多只能选择10项',
                  duration: 1500,
                  type: 'warning'
                })
                this.$nextTick(() => {
                  this.patentEngineer = [];
                  newVal.slice(0,10).forEach(item => {
                      this.patentEngineer.push(item);
                      ++this.patentKey;
                  });
                  this.removePatent(false)
                })
              };
            },            
            deep: true,
            immediate: true
        },
        'brandEngineer':{
            handler(newVal, oldVal){
              if (newVal.length > 10) {
                this.$message({
                  message: '最多只能选择10项',
                  duration: 1500,
                  type: 'warning'
                })
                this.$nextTick(() => {
                  this.brandEngineer = [];
                  newVal.slice(0,10).forEach(item => {
                      this.brandEngineer.push(item);
                      ++this.brandKey;
                  });
                  this.removeBrand(false)
                })
              };
            },            
            deep: true,
            immediate: true
        },
        'copyrightEngineer':{
            handler(newVal, oldVal){
              if (newVal.length > 10) {
                this.$message({
                  message: '最多只能选择10项',
                  duration: 1500,
                  type: 'warning'
                })
                this.$nextTick(() => {
                  this.copyrightEngineer = [];
                  newVal.slice(0,10).forEach(item => {
                      this.copyrightEngineer.push(item);
                      ++this.copyrightKey;
                  });
                  this.removeCopyright(false)
                })
              };
            },            
            deep: true,
            immediate: true
        },
        'otherEngineer':{
            handler(newVal, oldVal){
              if (newVal.length > 10) {
                this.$message({
                  message: '最多只能选择10项',
                  duration: 1500,
                  type: 'warning'
                })
                this.$nextTick(() => {
                  this.otherEngineer = [];
                  newVal.slice(0,10).forEach(item => {
                      this.otherEngineer.push(item);
                      ++this.otherKey;
                  });
                  this.removeOther(false)
                })
              };
            },            
            deep: true,
            immediate: true
        },
        'selectiveEngineer':{
            handler(newVal, oldVal){
              if (newVal.length > 50) {
                this.$message({
                  message: '最多只能选择50项',
                  duration: 1500,
                  type: 'warning'
                })
                this.$nextTick(() => {
                  this.selectiveEngineer = [];
                  newVal.slice(0,50).forEach(item => {
                      this.selectiveEngineer.push(item);
                      ++this.selectKey;
                  });
                })
              };              
            },
            deep: true,
            immediate: true
        },
        'selectList':{
            handler(newVal, oldVal){
              this.selectKey++;
            },
            deep: true,
            immediate: true
        },
    },
    
  methods: {
    getData() {
      // 组织架构
      getEmpList(false).then((res) => {
        this.companyList = res.data.data;
        this.recordList = res.data.data;
      });
      getEmpList(false).then((res) => {
        this.selectList = res.data.data;
      });
    },
    getAppoint(){
        let param = {
            start: this.page.currentPage,
            size: this.page.pageSize,
        }
        getList(param ).then((res) => {
            this.tableData = res.data.data.list;
            this.page.total = res.data.data.total;
        });
 
    },
    handldeChange(val){
      console.log(this.defaultEngineer,'iiii')
    },
    removeTag(val){
        var list = JSON.parse(JSON.stringify(this.appointPerson)); 
        this.appointPerson = [];
        if(list.length>1){
            list.slice(0,list.length-1).forEach(item => {
                this.appointPerson.push(item);
                ++this.refreshKey;
            });
        }else{
            ++this.refreshKey;
        };
    },
    removeDefault(callback){ //只有回调参数为false时才触发
      if(!callback){
        this.selectiveEngineer = []
        this.defaultEngineer.forEach((i,key)=>{        
          this.selectiveEngineer.push(i)  
        })       
        ++this.selectKey;
        this.selectiveEngineer = this.unique(this.selectiveEngineer)
        this.defaultEngineer.forEach(item=>{
          console.log(item)
          this.forTreeData(this.selectList,item[item.length-1])
        })
      }      
    },
    removePatent(callback){
      if(!callback){
        this.patentEngineer.forEach((i,key)=>{        
          this.selectiveEngineer.push(i)  
        })       
        ++this.selectKey;
        this.selectiveEngineer = this.unique(this.selectiveEngineer)
      }      
    },
    removeBrand(callback){
      if(!callback){
        this.brandEngineer.forEach((i,key)=>{        
          this.selectiveEngineer.push(i)  
        })       
        ++this.selectKey;
        this.selectiveEngineer = this.unique(this.selectiveEngineer)
      }       
    },
    removeCopyright(callback){
      if(!callback){
        this.copyrightEngineer.forEach((i,key)=>{        
          this.selectiveEngineer.push(i)  
        })       
        ++this.selectKey;
        this.selectiveEngineer = this.unique(this.selectiveEngineer)
      }      
    },
    removeOther(callback){
      if(!callback){
        this.otherEngineer.forEach((i,key)=>{        
          this.selectiveEngineer.push(i)  
        })       
        ++this.selectKey;
       this.selectiveEngineer = this.unique(this.selectiveEngineer)
      }      
    },
    unique(arr) {
      const res = new Map();
      return arr.filter((arr) => !res.has(arr[arr.length-1]) && res.set(arr[arr.length-1], 1))      
    },
    forTreeData(val, cValue) {
      val.forEach((item) => {
        if (item.customerId !== null && item.customerId == cValue) {
          item.disabled = true;
        }
        if (item.children !== null && item.children.length > 0) {
          this.forTreeData(item.children, cValue);
        }
      });
    },
    // 编辑
    handldEdit(row) {
        this.appointForm = row
        this.centerDialogVisible = true
        if(row.appointType && JSON.parse(row.appointType) && JSON.parse(row.appointType).length>0 && row.id != 6 && row.id != 8){
             this.notShow= true
             this.radio='2'
             this.appointPerson = JSON.parse(row.appointType)
        }else{
             this.notShow= true
             this.radio = '1'
            //  this.appointPerson = []
        }
        if(row.permissionName == "退款审批" || row.permissionName == '认证审批'){
          this.notShow= false
          this.radio='2'
        }
        if(row.defaultAppointType){
          this.defaultEngineer = JSON.parse(row.defaultAppointType)
        }  
        if(row.appointType && row.id == 8 ){
          this.selectiveEngineer = JSON.parse(row.appointType)
        }  
        if( row.id == 6 ){
          if( JSON.parse(row.appointType).length> 0){this.selectiveEngineer = JSON.parse(row.appointType);}
          if( JSON.parse(row.permissionEngineer.defaultPatentEngineerAppointType).length> 0){this.patentEngineer = JSON.parse(row.permissionEngineer.defaultPatentEngineerAppointType)}
          if( JSON.parse(row.permissionEngineer.defaultTrademarkEngineerAppointType).length> 0){this.brandEngineer = JSON.parse(row.permissionEngineer.defaultTrademarkEngineerAppointType)}
          if( JSON.parse(row.permissionEngineer.defaultCopyrightEngineerAppointType).length> 0){this.copyrightEngineer = JSON.parse(row.permissionEngineer.defaultCopyrightEngineerAppointType)}
          if( JSON.parse(row.permissionEngineer.defaultOtherEngineerAppointType).length> 0){this.otherEngineer = JSON.parse(row.permissionEngineer.defaultOtherEngineerAppointType)}                  
        }
    },
    // 确定
    handleUpdata(){      
        let customerNos = [];
        let defaultCustomerNos = [];
        let a = JSON.parse(JSON.stringify(this.appointPerson))
        let b = JSON.parse(JSON.stringify(this.selectiveEngineer))
        let c = JSON.parse(JSON.stringify(this.defaultEngineer))
        if(this.appointForm.id == 8 && b.length > 0){  //处理默认可选工程师
          b.forEach(element=>{
            customerNos.push(element[element.length-1])
          })
        }
        if(c && c.length>0){                            //处理默认工程师
          c.forEach(element=>{
            defaultCustomerNos.push(element[element.length-1])
          })
        }
        if(this.radio == 1 && this.appointForm.id != 8 && this.appointForm.id != 9){
          customerNos =[]
        } else if(this.appointForm.id != 8){
            if(a && a.length>0){
              a.forEach(element=>{
                customerNos.push(element[element.length-1])
              })
            }
        }
        if(this.appointForm.id == 8){
            this.params ={
              customerNos,
              defaultCustomerNos,
              appoints: this.selectiveEngineer,  // 回显处理字段
              defaultAppoints:this.defaultEngineer,
              id:this.appointForm.id
            }
        } else {
            this.params ={
                customerNos,
                appoints:this.radio==1 && this.appointForm.id!=9?[]:this.appointPerson,  // 回显处理字段
                id:this.appointForm.id
            }
        }
        editAppoint(this.params).then(res=>{
            if(res.data.code == 1000){
                this.$message({
                type: "success",
                message: "编辑成功!",
                });
                this.getAppoint()
                this.centerDialogVisible = false
            }
        })
    },
    //知产确定按钮
    handleProperty(){
      let permissionEngineer = {
        defaultPatentEngineerNos:[],
        defaultPatentEngineerAppoints: this.patentEngineer,
        defaultTrademarkEngineerNos:[],
        defaultTrademarkEngineerAppoints: this.brandEngineer,
        defaultCopyrightEngineerNos:[],
        defaultCopyrightEngineerAppoints: this.copyrightEngineer,
        defaultOtherEngineerNos:[],
        defaultOtherEngineerAppoints: this.otherEngineer,
      };
      let customerNos = [];
      let a = JSON.parse(JSON.stringify(this.patentEngineer));
      let b = JSON.parse(JSON.stringify(this.brandEngineer));
      let c = JSON.parse(JSON.stringify(this.copyrightEngineer));
      let d = JSON.parse(JSON.stringify(this.otherEngineer));
      let e = JSON.parse(JSON.stringify(this.selectiveEngineer))
      if( a.length > 0 && b.length > 0  && c.length > 0 && d.length > 0 && e.length > 0){
        a.forEach(i=>{
          permissionEngineer.defaultPatentEngineerNos.push(i[i.length-1])
        });
        b.forEach(i=>{
          permissionEngineer.defaultTrademarkEngineerNos.push(i[i.length-1])
        });
        c.forEach(i=>{
          permissionEngineer.defaultCopyrightEngineerNos.push(i[i.length-1])
        });
        d.forEach(i=>{
          permissionEngineer.defaultOtherEngineerNos.push(i[i.length-1])
        });
        e.forEach(i=>{
          customerNos.push(i[i.length-1])
        });
        let para = {
          customerNos,
          permissionEngineer,
          appoints: this.selectiveEngineer,
          id: this.appointForm.id
        }
        editAppoint(para).then(res=>{
            if(res.data.code == 1000){
                this.$message({
                  type: "success",
                  message: "编辑成功!",
                });
                this.getAppoint()
                this.centerDialogVisible = false
            }
        })
      } else {
        this.$message({
          type: "warning",
          message: "请选择必填项!",
          offset: 200
        });
      }
      
    },
    // 取消
    handleCancle(){
         this.centerDialogVisible = false
    },
    sizeChange(val) {
      this.page.currentPage = 1;
      this.page.pageSize = val;
      this.getAppoint();
    },
    currentChange(val) {
      this.page.currentPage = val;
      this.getAppoint();
    },
  },
};
</script>

<style scoped>
.tip{
  position: relative;
  top: -10px;
  left: 41%;
  color: #666666;
}
.teshu{
   left: 26%;
}
.name{
    margin: 6px 0 15px 15px;
}
.hot_title{
  font-size: 16px;
  font-weight: 550;
}
.parallel{
  margin-left: 10px;
}
.text {
  overflow: hidden;
  white-space: nowrap;
  -ms-text-overflow: ellipsis;
  text-overflow: ellipsis;
}
.orderMsg {
  display: flex;
  flex-direction: column;
}
.orangeName {
  color: #e6a23c;
}
.senior {
  margin: 10px 0px;
}
.search {
  margin: 25px 0px;
}
.radio-sty {
  margin-left: 20px;
}
.radio-sty-left {
  border-left: 1px solid #dcdfe6;
}
.cell-blue {
  color: #36a6fe;
  cursor: pointer;
}
.list-btn {
  padding: 8px 20px;
  margin: 0 5px;
  border: 1px solid #eee;
  border-radius: 5px;
  cursor: pointer;
}
.activebtn {
  background: #36a6fe;
  border-radius: 5px;
  border: 0;
  color: #fff;
}
.circleBlue {
  width: 6px;
  height: 6px;
  float: left;
  border-radius: 50%;
  background: #36a6fe;
  margin-top: 4px;
  margin-right: 7px;
}
.circleBluec {
  width: 6px;
  height: 6px;
  display: inline-block;
  border-radius: 50%;
  background: #36a6fe;
  margin-right: 7px;
}
.circleRed {
  background: red;
}
.circleRedc {
  width: 6px;
  height: 6px;
  display: inline-block;
  border-radius: 50%;
  margin-right: 7px;
  background: red;
}
.success {
  font-weight: bolder;
  font-size: 12px;
  float: left;
  color: green;
  margin-top: 2px;
  margin-right: 6px;
}
.successc {
  font-weight: bolder;
  font-size: 12px;
  color: green;
  margin-right: 6px;
}
.pagination {
  float: right;
}
.keyword {
  width: 350px;
}
.state-right {
  margin-right: 20px;
}
.radio-sty-left {
  border-left: 1px solid #dcdfe6;
}
</style>