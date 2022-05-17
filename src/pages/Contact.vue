<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('/img/contact-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="page-heading">
              <h1>联系我</h1>
              <!-- <span class="subheading">Have questions? I have answers.</span> -->
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <p>想联系我吗？请填写下面的表单给我留言，我会尽快给你回复！</p>
          <form name="sentMessage" id="contactForm" novalidate>
            <div class="control-group">
              <div class="form-group floating-label-form-group controls">
                <label>姓名</label>
                <input type="text" v-model="form.name" class="form-control" placeholder="姓名" id="name" required data-validation-required-message="Please enter your name.">
                <p class="help-block text-danger"></p>
              </div>
            </div>
            <div class="control-group">
              <div class="form-group floating-label-form-group controls">
                <label>邮箱</label>
                <input type="email" v-model="form.email" class="form-control" placeholder="邮箱地址" id="email" required data-validation-required-message="Please enter your email address.">
                <p class="help-block text-danger"></p>
              </div>
            </div>
            <div class="control-group">
              <div class="form-group col-xs-12 floating-label-form-group controls">
                <label>手机号</label>
                <input type="tel" v-model="form.phone" class="form-control" placeholder="手机号" id="phone" required data-validation-required-message="Please enter your phone number.">
                <p class="help-block text-danger"></p>
              </div>
            </div>
            <div class="control-group">
              <div class="form-group floating-label-form-group controls">
                <label>留言内容</label>
                <textarea rows="5" v-model="form.message" class="form-control" placeholder="留言内容" id="message" required data-validation-required-message="Please enter a message."></textarea>
                <p class="help-block text-danger"></p>
              </div>
            </div>
            <br>
            <div id="success"></div>
            <button type="button" @click='obSubmit' class="btn btn-primary" id="sendMessageButton">提交</button>
          </form>
        </div>
      </div>
    </div>
  </Layout>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'Contact',
    data: function() {
      return {
        form: {
          name: '',
          email: '',
          phone: '',
          message: '',
        }
      }
    },
    methods: {
      async obSubmit () {
        try {
          const { data } = await axios.post(`${this.GRIDSOME_PROXY_URL}/contacts`, this.form)
          this.form = {
            name: '',
            email: '',
            phone: '',
            message: '',
          }
          window.alert('发送成功')
        } catch (err) {
          window.alert('发送失败，请稍后重试')
        }
      }
    }
  }
</script>

<style>

</style>