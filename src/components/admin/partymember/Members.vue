<template>
  <div>
    <el-row style="margin: 18px 0px 0px 18px ">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/admin/dashboard' }">管理中心</el-breadcrumb-item>
        <el-breadcrumb-item>人口管理</el-breadcrumb-item>
        <el-breadcrumb-item>党员管理</el-breadcrumb-item>
      </el-breadcrumb>
    </el-row>
    <edit-form @onSubmit="loadBooks()" ref="edit"></edit-form>
    <el-card style="margin: 18px 2%;width: 95%">
      <el-table
        :data="residents"
        stripe
        style="width: 100%"
        :max-height="tableHeight">
        <el-table-column
          type="selection"
          width="55">
        </el-table-column>
        <!--        <el-table-column type="expand">-->
        <!--          <template slot-scope="props">-->
        <!--            <el-form label-position="left" inline>-->
        <!--              <el-form-item>-->
        <!--                <span>{{ props.row.photo }}</span>-->
        <!--              </el-form-item>-->
        <!--            </el-form>-->
        <!--          </template>-->
        <!--        </el-table-column>-->
        <el-table-column
          prop="name"
          label="姓名"
          fit>
        </el-table-column>
        <el-table-column
          prop="sex"
          label="性别"
          fit>
        </el-table-column>
        <el-table-column
          prop="branchpost"
          label="现任党内职务"
          fit>
        </el-table-column>
        <el-table-column
          prop="birthdate"
          label="生日"
          fit>
        </el-table-column>
        <el-table-column
          prop="address"
          label="家庭住址"
          fit>
        </el-table-column>
        <!--        <el-table-column-->
        <!--          prop="abs"-->
        <!--          label="摘要"-->
        <!--          show-overflow-tooltip-->
        <!--          fit>-->
        <!--        </el-table-column>-->
        <el-table-column
          fixed="right"
          label="操作"
          width="120">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="editBook(scope.row)"
              type="text"
              size="small">
              编辑
            </el-button>
            <el-button
              @click.native.prevent="deleteBook(scope.row.id)"
              type="text"
              size="small">
              移除
            </el-button>
          </template>
        </el-table-column>
      </el-table>
      <div style="margin: 20px 0 20px 0;float: left">
        <el-button>取消选择</el-button>
        <el-button>批量删除</el-button>
      </div>
    </el-card>
  </div>
</template>

<script>
  import EditForm from './EditForm'
  export default {
    name: 'Members',
    components: {EditForm},
    data () {
      return {
        residents: []
      }
    },
    mounted () {
      this.loadBooks()
    },
    computed: {
      tableHeight () {
        return window.innerHeight - 320
      }
    },
    methods: {
      deleteBook (id) {
        this.$confirm('此操作将永久删除该党员信息, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
            this.$axios
              .post('/admin/people/residents/delete', {id: id}).then(resp => {
              if (resp && resp.data.code === 200) {
                this.loadBooks()
              }
            })
          }
        ).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          })
        })
      },
      editBook (item) {
        this.$refs.edit.dialogFormVisible = true
        this.$refs.edit.form = {
          id: item.id,
          name: item.name,
          sex: item.sex,
          birthdate: item.birthdate,
          natived: item.natived,
          naplace: item.naplace,
          beregulartime: item.beregulartime,
          joinworktime: item.joinworktime,
          idnum: item.idnum,
          photo: item.photo,
          joinpartybranch: item.joinpartybranch,
          jpintroducer: item.jpintroducer,
          inbranchtime: item.inbranchtime,
          outbranch: item.outbranch,
          branchpost: item.branchpost,
          joinpartytime: item.joinpartytime,
          edudegree: item.edudegree,
          gradschmajor: item.gradschmajor,
          unitpost: item.unitpost,
          registerplace: item.registerplace,
          address: item.address,
          phone: item.phone
        }
        // this.$refs.edit.category = {
        //   id: item.category.id.toString()
        // }
      },
      loadBooks () {
        var _this = this
        this.$axios.get('/residents').then(resp => {
          if (resp && resp.status === 200) {
            _this.residents = resp.data
          }
        })
      }
    }
  }
</script>

<style scoped>
</style>
