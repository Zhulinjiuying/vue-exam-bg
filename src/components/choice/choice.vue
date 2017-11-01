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
        num: 1
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
      },
      subItem() {
        if (this.num > 0) {
          this.num = this.num - 1
        }
      }
    },
    computed: {
      questionsItem: function() {
        return Array.from({length: this.num}, () => { return {} })
      }
    },
    watch: {
      'num': function(newValue, oldValue) {
        if (newValue > oldValue) {
          this.questionsItem.push({})
        } else {
          this.questionsItem.pop()
        }
      },
      'item': function() {
        if (!this.questions) {
          this.questions = Array.from({length: this.num}, () => { return {} })
        }
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
</style>