<template>
  <div class="single">
    <el-form-item :label="title">
      <el-input v-model="t_question.title" placeholder="请输入题目信息"></el-input>
    </el-form-item>
    <el-form-item label="选项A:">
      <el-input v-model="t_question.item[0]" placeholder="请输入选项"></el-input>
    </el-form-item>
    <el-form-item label="选项B:">
      <el-input v-model="t_question.item[1]" placeholder="请输入选项"></el-input>
    </el-form-item>
    <el-form-item label="选项C:">
      <el-input v-model="t_question.item[2]" placeholder="请输入选项"></el-input>
    </el-form-item>
    <el-form-item label="选项D:">
      <el-input v-model="t_question.item[3]" placeholder="请输入选项"></el-input>
    </el-form-item>
    <el-form-item label="正确答案是">
      <el-radio class="radio" v-model="t_question.answer" label="1">A</el-radio>
      <el-radio class="radio" v-model="t_question.answer" label="2">B</el-radio>
      <el-radio class="radio" v-model="t_question.answer" label="3">C</el-radio>
      <el-radio class="radio" v-model="t_question.answer" label="4">D</el-radio>
    </el-form-item>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        t_question: {
          title: '',
          item: ['', '', '', ''],
          answer: '1'
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
      if (this.question.item) {
        for (let i = 0; i < this.question.item.length; i++) {
          if (this.question.item[i]) {
            this.t_question.item[i] = this.question.item[i]
          }
        }
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
      this.question.item = []
      for (let i = 0; i < this.t_question.item.length; i++) {
        if (this.t_question.item[i]) {
          this.question.item[i] = this.t_question.item[i]
        }
      }
      if (this.t_question.answer) {
        this.question.answer = this.t_question.answer
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
</style>