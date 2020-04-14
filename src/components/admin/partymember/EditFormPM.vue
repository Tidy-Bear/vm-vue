<template>
  <div>
    <i class="el-icon-circle-plus-outline"  @click="dialogFormVisible = true"></i>
    <el-dialog
      title="添加/修改党员信息"
      :visible.sync="dialogFormVisible"
      style="max-width: 8000px"
      @close="clear">
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="150px" class="demo-ruleForm">
          <el-form-item prop="id" style="height: 0">
            <el-input type="hidden" v-model="ruleForm.id" autocomplete="off"></el-input>
          </el-form-item>
          <el-form-item label="姓名" prop="name">
            <el-input v-model="ruleForm.name"></el-input>
          </el-form-item>
          <el-form-item label="身份证" prop="idnum">
            <el-input v-model="ruleForm.idnum"></el-input>
          </el-form-item>
          <el-form-item label="民族" prop="natived">
            <el-input v-model="ruleForm.natived"></el-input>
          </el-form-item>
          <el-form-item label="性别" prop="sex">
            <el-select v-model="ruleForm.sex" placeholder="请选择性别">
              <el-option label="男" value="男"></el-option>
              <el-option label="女" value="女"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="出生日期" required>
            <el-col :span="11">
              <el-form-item prop="date">
                <el-date-picker type="date" placeholder="选择日期" v-model="ruleForm.birthdate" style="width: 100%;"></el-date-picker>
              </el-form-item>
            </el-col>
          </el-form-item>
          <el-form-item label="正面免冠照片" prop="photo">
            <el-input v-model="ruleForm.photo" autocomplete="off"></el-input>
            <img-upload @onUpload="uploadImg" ref="imgUpload"></img-upload>
          </el-form-item>
          <el-form-item label="籍贯" prop="naplace">
            <el-input v-model="ruleForm.naplace" autocomplete="off" ></el-input>
          </el-form-item>
          <el-form-item label="毕业院校及专业" prop="gradschmajor">
            <el-input v-model="ruleForm.gradschmajor" autocomplete="off" ></el-input>
          </el-form-item>
          <el-form-item label="现工作单位及职务" prop="unitpost">
            <el-input v-model="ruleForm.unitpost" autocomplete="off" ></el-input>
          </el-form-item>
          <el-form-item label="现任党内职务" prop="branchpost">
            <el-input v-model="ruleForm.branchpost" autocomplete="off" ></el-input>
          </el-form-item>
          <el-form-item label="户籍所在地" prop="registerplace">
            <el-input v-model="ruleForm.registerplace" autocomplete="off" ></el-input>
          </el-form-item>
          <el-form-item label="手机号码" prop="phone">
            <el-input v-model="ruleForm.phone" autocomplete="off" ></el-input>
          </el-form-item>
            <el-form-item label="家庭住址" prop="address" >
              <el-input v-model="ruleForm.address" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="文化程度" prop="edudegree">
              <el-select v-model="ruleForm.edudegree" placeholder="请选择文化程度">
                <el-option label="小学" value="小学"></el-option>
                <el-option label="初中" value="初中"></el-option>
                <el-option label="高中" value="高中"></el-option>
                <el-option label="中专" value="中专"></el-option>
                <el-option label="本科" value="本科"></el-option>
                <el-option label="硕士" value="硕士"></el-option>
                <el-option label="博士" value="博士"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="入党时间" prop="joinpartytime">
              <div class="block">
                <el-date-picker
                  v-model="ruleForm.joinpartytime"
                  type="date"
                  placeholder="何时转正">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="转正时间" prop="beregulartime">
              <div class="block">
                <el-date-picker
                  v-model="ruleForm.beregulartime"
                  type="date"
                  placeholder="何时转正">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="入党介绍人" prop="jointroducer" >
              <el-input v-model="ruleForm.jointroducer" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="入党时所在支部" prop="joinpartybranch" >
              <el-input v-model="ruleForm.joinpartybranch" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="转入当前党支部日期" prop="inbranchtime">
              <div class="block">
                <el-date-picker
                  v-model="ruleForm.inbranchtime"
                  type="date"
                  placeholder="何时转入当前党支部">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="参加工作时间" prop="joinworktime">
              <div class="block">
                <el-date-picker
                  v-model="ruleForm.joinworktime"
                  type="date"
                  placeholder="何时参加工作">
                </el-date-picker>
              </div>
            </el-form-item>
            <el-form-item label="转出党支部名称" prop="outbranch" >
              <el-input v-model="ruleForm.outbranch" autocomplete="off"></el-input>
            </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
            <el-button @click="resetForm('ruleForm')">重置</el-button>
          </el-form-item>
        </el-form>
        </el-dialog>
      </div>
</template>

<script>
  import ImgUpload from './ImgUploadPM'
  export default {
    name: 'EditFormPM',
    components: {ImgUpload},
    data () {
      return {
        dialogFormVisible: false,
        ruleForm: {
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
        rules: {
          name: [
            { required: true, message: '请输入姓名', trigger: 'blur' }
          ],
          natived: [
            { required: true, message: '请输入民族', trigger: 'blur' }
          ],
          naplace: [
            { required: true, message: '请输入籍贯', trigger: 'blur' }
          ],
          idnum: [
            { required: true, message: '请输入身份证', trigger: 'blur' }
          ],
          joinpartybranch: [
            { required: true, message: '请输入入党时所在支部', trigger: 'blur' }
          ],
          jointroducer: [
            { required: true, message: '请输入入党介绍人', trigger: 'blur' }
          ],
          outbranch: [
            { required: true, message: '请输入转出党支部名称', trigger: 'blur' }
          ],
          branchpost: [
            { required: true, message: '请输入现任党内职务', trigger: 'blur' }
          ],
          gradschmajor: [
            { required: true, message: '请输入毕业院校及专业', trigger: 'blur' }
          ],
          unitpost: [
            { required: true, message: '请输入现工作单位职务', trigger: 'blur' }
          ],
          registerplace: [
            { required: true, message: '请输入户籍所在地', trigger: 'blur' }
          ],
          address: [
            { required: true, message: '请输入家庭住址', trigger: 'blur' }
          ],
          phone: [
            { required: true, message: '请输入电话号码', trigger: 'blur' }
          ],
          sex: [
            { required: true, message: '请选择性别', trigger: 'change' }
          ],
          birthdate: [
            { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
          ],
          beregulartime: [
            { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
          ],
          joinworktime: [
            { required: true, message: '请选择日期', trigger: 'change' }
          ],
          inbranchtime: [
            { required: true, message: '请选择日期', trigger: 'change' }
          ],
          joinpartytime: [
            { required: true, message: '请选择日期', trigger: 'change' }
          ],
          edudegree: [
            { required: true, message: '请选择教育程度', trigger: 'change' }
          ]
        }
      }
    },
    methods: {
      submitForm (formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.$axios
              .put('/admin/partymember/members', {
                id: this.ruleForm.id,
                name: this.ruleForm.name,
                sex: this.ruleForm.sex,
                birthdate: this.ruleForm.birthdate,
                natived: this.ruleForm.natived,
                naplace: this.ruleForm.naplace,
                beregulartime: this.ruleForm.beregulartime,
                joinworktime: this.ruleForm.joinworktime,
                idnum: this.ruleForm.idnum,
                photo: this.ruleForm.photo,
                joinpartybranch: this.ruleForm.joinpartybranch,
                jointroducer: this.ruleForm.jointroducer,
                inbranchtime: this.ruleForm.inbranchtime,
                outbranch: this.ruleForm.outbranch,
                branchpost: this.ruleForm.branchpost,
                joinpartytime: this.ruleForm.joinpartytime,
                edudegree: this.ruleForm.edudegree,
                address: this.ruleForm.address,
                gradschmajor: this.ruleForm.gradschmajor,
                unitpost: this.ruleForm.unitpost,
                registerplace: this.ruleForm.registerplace,
                phone: this.ruleForm.phone
              }).then(resp => {
              if (resp && resp.status === 200) {
                this.dialogFormVisible = false
                this.$emit('submitForm')
                location.reload()
                this.$router.go(0)
              }
            })
          } else {
            console.log('error submit!!')
            return false
          }
        })
      },
      resetForm (formName) {
        this.$refs[formName].resetFields()
      }
    },
    uploadImg () {
      this.ruleForm.photo = this.$refs.imgUpload.url
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
