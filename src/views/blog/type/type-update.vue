<template>
  <div>
    <el-form ref="form" :rules="rules" :model="temp" label-width="80px" size="mini">
      <el-form-item label="分类名" prop="typeName">
        <el-input v-model="temp.typeName" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" size="mini" @click="save">提交</el-button>
        <el-button size="mini" @click="cancel">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import typeApi from '@/api/type'
export default {
  props: {
    type: {
      type: Object,
      default: null
    }
  },
  data() {
    return {
      temp: { },
      rules: {
        typeName: [{ required: true, message: '* is required', trigger: 'blur' }]
      }
    }
  },
  created() {
    this.temp = this.type
  },
  methods: {
    save() {
      this.$refs['form'].validate((valid) => {
        if (valid) {
          typeApi.update(this.temp).then(res => {
            this.$message.success(res.msg)
            this.$emit('closeUpdateDialog')
            this.$emit('getTypeList')
          })
        }
      })
    },
    cancel() {
      this.$emit('closeUpdateDialog')
      this.$emit('getTypeList')
    }
  }
}
</script>
