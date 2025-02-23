<template>
  <div>
    <el-form ref="formRef" :model="formData" :rules="rules" size="default" label-width="100px">
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程编号" prop="code">
            <el-input v-model="formData.code" type="text" placeholder="请输入课程编号" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="课程学科" prop="subject">
            <el-select v-model="formData.subject" placeholder="请选择课程学科" clearable :style="{width: '100%'}">
              <el-option v-for="(item, index) in subjectOptions" :key="index" :label="item.label"
                :value="item.value" :disabled="item.disabled"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程价格" prop="field114">
            <el-input v-model="formData.field114" type="text" placeholder="请输入课程价格" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="课程名称" prop="field113">
            <el-input v-model="formData.field113" type="text" placeholder="请输入课程名称" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="适用人群" prop="field116">
            <el-input v-model="formData.field116" type="text" placeholder="请输入适用人群" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="课程有效期" prop="field117">
            <el-date-picker type="daterange" v-model="formData.field117" format="YYYY-MM-DD"
              value-format="YYYY-MM-DD" :style="{width: '100%'}" start-placeholder="开始日期"
              end-placeholder="结束日期" range-separator="至" clearable></el-date-picker>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程封面" prop="field119" required>
            <el-upload ref="field119" :file-list="field119fileList" :action="field119Action"
              :before-upload="field119BeforeUpload">
              <el-button size="small" type="primary" icon="el-icon-upload">点击上传</el-button>
            </el-upload>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="推荐指数" prop="field120">
            <el-rate v-model="formData.field120"></el-rate>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-form-item label="课程介绍" prop="field122">
          <el-input v-model="formData.field122" type="textarea" placeholder="请输入课程介绍"
            :autosize="{minRows: 4, maxRows: 4}" :style="{width: '100%'}"></el-input>
        </el-form-item>
      </el-row>
      <el-form-item>
        <el-button type="primary" @click="submitForm">提交</el-button>
        <el-button @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script setup>
import {
  ElMessage
}
from 'element-plus'
const formRef = ref()
const data = reactive({
  formData: {
    code: undefined,
    subject: undefined,
    field114: undefined,
    field113: undefined,
    field116: undefined,
    field117: null,
    field119: null,
    field120: 0,
    field122: undefined,
  },
  rules: {
    code: [{
      required: true,
      message: '请输入课程编号',
      trigger: 'blur'
    }],
    subject: [{
      required: true,
      message: '请选择课程学科',
      trigger: 'change'
    }],
    field114: [{
      required: true,
      message: '请输入课程价格',
      trigger: 'blur'
    }],
    field113: [{
      required: true,
      message: '请输入课程名称',
      trigger: 'blur'
    }],
    field116: [{
      required: true,
      message: '请输入适用人群',
      trigger: 'blur'
    }],
    field117: [{
      required: true,
      message: '课程有效期不能为空',
      trigger: 'change'
    }],
    field120: [{
      required: true,
      message: '推荐指数不能为空',
      trigger: 'change'
    }],
    field122: [{
      required: true,
      message: '请输入课程介绍',
      trigger: 'blur'
    }],
  }
})
const {
  formData,
  rules
} = toRefs(data)
const subjectOptions = ref([{
  "label": "选项一",
  "value": 1
}, {
  "label": "选项二",
  "value": 2
}])
// 上传请求路径
const field119Action = ref('https://jsonplaceholder.typicode.com/posts/')
// 上传文件列表
const field119fileList = ref([])
/**
 * @name: 上传之前的文件判断
 * @description: 上传之前的文件判断，判断文件大小文件类型等
 * @param {*} file
 * @return {*}
 */
function field119BeforeUpload(file) {
  let isRightSize = file.size / 1024 / 1024 < 2
  if (!isRightSize) {
    ElMessage.error('文件大小超过 2MB')
  }
  return isRightSize
}
/**
 * @name: 表单提交
 * @description: 表单提交方法
 * @return {*}
 */
function submitForm() {
  formRef.value.validate((valid) => {
    if (!valid) return
    // TODO 提交表单
  })
}
/**
 * @name: 表单重置
 * @description: 表单重置方法
 * @return {*}
 */
function resetForm() {
  formRef.value.resetFields()
}

</script>
<style>
.el-upload__tip {
  line-height: 1.2;
}

.el-rate {
  display: inline-block;
  vertical-align: text-top;
}

</style>
