<template>
  <el-form labelPosition="left" label-width="100px">
    <component :is="item" v-for="n in num" :question="questionsItem[n - 1]" :index="n" :key="n">
    </component>
    <el-form-item>
      <el-button type="success" icon="el-icon-circle-plus" @click="addItem">添加一条</el-button>
      <el-button type="danger" icon="el-icon-remove" @click="subItem">减少一条</el-button>
    </el-form-item>
  </el-form>
</template>
<script>
  import MultipleChoice from '@/components/multiplechoice/multiplechoice.vue'
  import SingleChoice from '@/components/singlechoice/singlechoice.vue'
  import TfChoice from '@/components/tfchoice/tfchoice.vue'

  export default {
    data() {
      return {
        num: 1,
        questionsItem: '',
        t_item: ''
      }
    },
    props: {
      questions: {
        type: Array
      },
      item: {
        type: String,
        default: 'SingleChoice'
      }
    },
    components: {
      SingleChoice,
      MultipleChoice,
      TfChoice
    },
    methods: {
      addItem() {
        this.num = this.num + 1
        this.questionsItem.push({})
      },
      subItem() {
        if (this.num > 0) {
          this.num = this.num - 1
          this.questionsItem.pop()
        }
      }
    },
    created: function() {
      this.t_item = this.item
      if (this.questions.length === 0) {
        this.questionsItem = Array.from({length: this.num}, () => { return {} })
      } else {
        this.questionsItem = this.questions
        this.num = this.questions.length
      }
    },
    beforeUpdate: function() {
      if (this.t_item === this.item) {
        return
      } else {
        this.t_item = this.item
      }
      if (this.questions.length > 0) {
        this.num = this.questions.length
        this.questionsItem = this.questions
      } else {
        this.num = 1
        this.questionsItem = Array.from({length: this.num}, () => { return {} })
      }
    },
    watch: {
      'questionsItem': function() {
        this.$emit('update:questions', this.questionsItem)
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
</style>