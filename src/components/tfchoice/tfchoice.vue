<template>
  <div class="tf">
    <el-form-item :label="title">
      <el-input v-model="t_question.title" placeholder="请输入题目信息"></el-input>
    </el-form-item>
    <el-form-item label="正确答案是">
      <el-radio class="radio" v-model="t_question.answer" label="1">对</el-radio>
      <el-radio class="radio" v-model="t_question.answer" label="2">错</el-radio>
    </el-form-item>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        t_question: {
          title: '',
          answer: ''
        }
      }
    },
    props: {
      question: {
        type: Object
      },
      index: {
        type: Number
      }
    },
    created: function() {
      if (this.question.title) {
        this.t_question.title = this.question.title
      }
      if (this.question.answer) {
        this.t_question.answer = this.question.answer
      }
    },
    computed: {
      title: function() {
        return this.index + '.题目'
      }
    },
    beforeDestroy: function() {
      if (this.t_question.title) {
        this.question.title = this.t_question.title
      }
      if (this.t_question.answer) {
        this.question.answer = this.t_question.answer
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
</style>