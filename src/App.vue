<template>
  <div id="app">
    <header class="header" :class="{ 'header-fixed' : headerFixed }">
      <el-form :inline="true" class="form-inline">
        <h1>考试系统后台配置</h1>
      </el-form>
    </header>
    <div v-show="headerFixed" style="position: relative;height: 60px;width: 100%;"></div>
    <main>
      <div class="main-left">
        <el-menu default-active="/singleQuesitions" class="el-menu-vertical-demo" :router="true">
          <el-menu-item index="/singleQuesitions" :class="{'isActive': active === 1}">单项选择题</el-menu-item>
          <el-menu-item index="/multipleQuesitions" :class="{'isActive': active === 2}">多项选择题</el-menu-item>
          <el-menu-item index="/tfQuesitions" :class="{'isActive': active === 3}">判断题</el-menu-item>
        </el-menu>
      </div>
      <div  class="main-right" >
        <transition name="fade">
          <router-view class="view" :item="item" :questions.sync="questions[item]"></router-view>
        </transition>
        <el-button type="primary" @click="onSubmit">提交</el-button>
      </div>
    </main>
  </div>
</template>

<script>
  import Vue from 'vue'
  import Element from 'element-ui'
  import 'element-ui/lib/theme-chalk/index.css'

  Vue.use(Element)

  export default {
    data() {
      return {
        headerFixed: true,
        active: 1,
        item: 'SingleChoice',
        questions: {
          SingleChoice: [],
          MultipleChoice: [],
          TfChoice: []
        }
      }
    },
    created: function() {
      this.$router.push('/singleQuesitions')
    },
    methods: {
      onSubmit() {

      }
    },
    watch: {
      '$route': function (to, from) {
        if (to.path === '/singleQuesitions') {
          this.active = 1
          this.item = 'SingleChoice'
        } else if (to.path === '/multipleQuesitions') {
          this.active = 2
          this.item = 'MultipleChoice'
        } else if (to.path === '/tfQuesitions') {
          this.active = 3
          this.item = 'TfChoice'
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  body
    margin: 0
  #app 
    min-width: 1200px
    margin: 0 auto
    font-family: "Helvetica Neue","PingFang SC",Arial,sans-serif;
    header
      z-index: 1000
      min-width: 1200px
      transition: all 0.5s ease
      border-top: solid 4px #3091F2 
      background-color: #fff
      box-shadow: 0 2px 4px 0 rgba(0,0,0,.12),0 0 6px 0 rgba(0,0,0,.04)
      .form-inline
        margin-top: 5px
        padding-left: 300px!important;
      .header-fixed:
        position: fixed
        top: 0
        left: 0
        right: 0
    main
      display: flex
      min-height: 800px;
      border: solid 40px #E9ECF1  
      background-color: #FCFCFC
      .main-left
        text-align: center
        flex: 0 0 200px
      .main-right 
        -webkit-box-flex:1
        -ms-flex:1;flex:1
        background-color: #fff
        padding: 50px 70px
</style>
