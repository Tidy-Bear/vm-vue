<template>
  <div>
    <i class="el-icon-circle-plus-outline"  @click="dialogFormVisible = true"></i>
    <el-dialog
      title="添加/修改党员信息"
      :visible.sync="dialogFormVisible"
      style="max-width: 8000px"
      @close="clear">
      <el-form v-model="form" style="text-align: left;" ref="dataForm">
        <el-row :gutter="40">
          <el-col :span="15">
            <el-form-item prop="id" style="height: 0">
              <el-input type="hidden" v-model="form.id" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="姓名" :label-width="formLabelWidth" prop="name">
              <el-input v-model="form.name" autocomplete="off" ></el-input>
            </el-form-item>
            <el-form-item label="身份证" :label-width="formLabelWidth" prop="idnum">
              <el-input v-model="form.idnum" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="性别" :label-width="formLabelWidth" prop="sex">
              <el-select v-model="form.sex" placeholder="请选择性别">
                <el-option label="男" value="男"></el-option>
                <el-option label="女" value="女"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="民族" :label-width="formLabelWidth" prop="natived">
              <el-input v-model="form.natived" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="出生日期" :label-width="formLabelWidth" prop="date">
              <div class="block">
                <el-date-picker
                  v-model="form.birthdate"
                  type="date"
                  placeholder="选择出生日期">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="正面免冠照片" :label-width="formLabelWidth" prop="photo">
              <el-input v-model="form.photo" autocomplete="off"></el-input>
              <img-upload @onUpload="uploadImg" ref="imgUpload"></img-upload>
            </el-form-item>
            <el-form-item label="籍贯" :label-width="formLabelWidth" prop="naplace">
              <el-input v-model="form.naplace" autocomplete="off" ></el-input>
            </el-form-item>
            <el-form-item label="毕业院校及专业" :label-width="formLabelWidth" prop="gradschmajor">
              <el-input v-model="form.gradschmajor" autocomplete="off" ></el-input>
            </el-form-item>
            <el-form-item label="现工作单位及职务" :label-width="formLabelWidth" prop="unitpost">
              <el-input v-model="form.unitpost" autocomplete="off" ></el-input>
            </el-form-item>
            <el-form-item label="户籍所在地" :label-width="formLabelWidth" prop="registerplace">
              <el-input v-model="form.registerplace" autocomplete="off" ></el-input>
            </el-form-item>
            <el-form-item label="手机号码" :label-width="formLabelWidth" prop="phone">
              <el-input v-model="form.phone" autocomplete="off" ></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="15">
            <el-form-item label="家庭住址" :label-width="formLabelWidth" prop="address" >
              <el-input v-model="form.address" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="文化程度" :label-width="formLabelWidth" prop="edudegree">
              <el-select v-model="form.edudegree" placeholder="请选择文化程度">
                <el-option label="小学" value="小学"></el-option>
                <el-option label="初中" value="初中"></el-option>
                <el-option label="高中" value="高中"></el-option>
                <el-option label="中专" value="中专"></el-option>
                <el-option label="本科" value="本科"></el-option>
                <el-option label="硕士" value="硕士"></el-option>
                <el-option label="博士" value="博士"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="入党时间" :label-width="formLabelWidth" prop="joinpartytime" >
              <el-input v-model="form.joinpartytime" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="转正时间" :label-width="formLabelWidth" prop="beregulartime">
              <div class="block">
                <el-date-picker
                  v-model="form.beregulartime"
                  type="date"
                  placeholder="何时转正">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="入党介绍人" :label-width="formLabelWidth" prop="joinpartybranch" >
              <el-input v-model="form.jointroducer" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="入党时所在支部" :label-width="formLabelWidth" prop="joinpartybranch" >
              <el-input v-model="form.joinpartybranch" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="转入当前党支部日期" :label-width="formLabelWidth" prop="inbranchtime">
              <div class="block">
                <el-date-picker
                  v-model="form.inbranchtime"
                  type="date"
                  placeholder="何时转入当前党支部">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="参加工作时间" :label-width="formLabelWidth" prop="joinworktime">
              <div class="block">
                <el-date-picker
                  v-model="form.joinworktime"
                  type="date"
                  placeholder="何时参加工作">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="转出党支部名称" :label-width="formLabelWidth" prop="outbranch" >
              <el-input v-model="form.outbranch" autocomplete="off"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="onSubmit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import ImgUpload from './ImgUploadPM'
  export default {
    name: 'EditForm',
    components: {ImgUpload},
    data () {
      return {
        dialogFormVisible: false,
        form: {
          id: '',
          name: '',
          sex: '',
          birthdate: '',
          natived: '',
          naplace: '',
          beregulartime: '',
          joinworktime: '',
          idnum: '',
          photo: '',
          joinpartybranch: '',
          jointroducer: '',
          inbranchtime: '',
          outbranch: '',
          branchpost: '',
          joinpartytime: '',
          edudegree: '',
          gradschmajor: '',
          unitpost: '',
          registerplace: '',
          address: '',
          phone: ''
        },
        formLabelWidth: '160px'
      }
    },
    methods: {
      clear () {
        this.form = {
            id: '',
            name: '',
            sex: '',
            birthdate: '',
            natived: '',
            naplace: '',
            beregulartime: '',
            joinworktime: '',
            idnum: '',
            photo: '',
            joinpartybranch: '',
            jointroducer: '',
            inbranchtime: '',
            outbranch: '',
            branchpost: '',
            joinpartytime: '',
            edudegree: '',
            gradschmajor: '',
            unitpost: '',
            registerplace: '',
            address: '',
            phone: ''
        }
      },
      uploadImg () {
        this.form.photo = this.$refs.imgUpload.url
      },
      onSubmit () {
        this.$axios
          .put('/admin/partymember/members', {
            id: this.form.id,
            name: this.form.name,
            sex: this.form.sex,
            birthdate: this.form.birthdate,
            natived: this.form.natived,
            naplace: this.form.naplace,
            beregulartime: this.form.beregulartime,
            joinworktime: this.form.joinworktime,
            idnum: this.form.idnum,
            photo: this.form.photo,
            joinpartybranch: this.form.joinpartybranch,
            jointroducer: this.form.jointroducer,
            inbranchtime: this.form.inbranchtime,
            outbranch: this.form.outbranch,
            branchpost: this.form.branchpost,
            joinpartytime: this.form.joinpartytime,
            edudegree: this.form.edudegree,
            address: this.form.address,
            gradschmajor: this.form.gradschmajor,
            unitpost: this.form.unitpost,
            registerplace: this.form.registerplace,
            phone: this.form.phone
          }).then(resp => {
          if (resp && resp.status === 200) {
            this.dialogFormVisible = false
            this.$emit('onSubmit')
          }
        })
      }
    }
  }
</script>

<style scoped>
  .add-button {
    margin: 18px 0 0 10px;
  }
</style>
