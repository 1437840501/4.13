<template>

<div class="home">


<el-button type="text" @click="dialogFormVisible = true">点击修改</el-button>

<el-dialog title="表" :visible.sync="dialogFormVisible">
  <el-form :model="form">
    <el-form-item label="星期一" :label-width="formLabelWidth">
      <el-input v-model="form.one" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期二" :label-width="formLabelWidth">
      <el-input v-model="form.two" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期三" :label-width="formLabelWidth">
      <el-input v-model="form.three" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期四" :label-width="formLabelWidth">
      <el-input v-model="form.four" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期五" :label-width="formLabelWidth">
      <el-input v-model="form.five" auto-complete="off"></el-input>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="update">确 定</el-button>
  </div>
</el-dialog>

  <el-table
    :data="arr"
    style="width: 100%"
    height="500">
    <el-table-column
      fixed
      prop="data"
      label="时间\星期"
      width="150">
    </el-table-column>
    <el-table-column
      prop="yi"
      label="一"
      width="120">
    </el-table-column>
    <el-table-column
      prop="er"
      label="二"
      width="120">
    </el-table-column>
    <el-table-column
      prop="san"
      label="三"
      width="120">
    </el-table-column>
    <el-table-column
      prop="si"
      label="四"
      width="120">
    </el-table-column>
    <el-table-column
      prop="wu"
      label="五"
      width="120">
    </el-table-column>
<el-table-column
      fixed="right"
      label="操作"
      width="120">
    <template slot-scope="scope">

        <el-button @click="Delete(scope.row)" type="text"size="small">
          移除
        </el-button>
      </template>

</el-table-column>

  </el-table>


</div>
</template>

<script>
export default {

  props: {
    msg: String
  },
   created(){
      this.hehe()
      },
      data(){
      return{
      keyword:'fa',
      arr:[],
      dialogFormVisible: false,
          form:{
            yi:"",
            er:""
            san:"",
            si:"",
            wu:""
          },
          formLabelWidth:"120px"
        }

      
      },
       methods:{
       hehe(){
       this.$http.get('http://localhost:3000').then(e=>this.arr=e.body)
       },
       Delete(row){
      console.log(row)
         this.$http.post('http://localhost:3000/sc',{id:row.id},{emulateJSON:true}).then(e=>row.id=e.body)
        var _index =this.arr.indexOf(row)
        this.arr.splice(_index,1)
      },
      submit(){
          this.dialogFormVisible = false
          this.$http.post('http://localhost:3000/add',this.form,{emulateJSON:true}).then(function(){
            this.hehe()
            this.form={}
            this.$message({
          message: '恭喜你，这是一条成功消息',
          type: 'success'
        });
          })
        },
        tanchu(){
          this.dialogFormVisible = true
        },
        }
      }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
