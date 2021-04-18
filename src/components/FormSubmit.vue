<template>
  <div>
    <div>
      <my-logo :title='title'>
      </my-logo>
      <input type="button" @click="change_title" value="点击修改标题"/><br/>
    </div>
    <textarea v-model='content'>
    </textarea>
    <br/>
    <input type='button' @click='submit' value='留言'/>
  </div>
</template>

<script>
import MyLogo from './Logo.vue'
export default {
  data () {
    return {
      content: '',
      title: ''
    }
  },
  methods: {
    submit: function () {
      this.$http.post('/api/interface/blogs/add_comment',
        {
          content: this.content
        }
      )
        .then((response) => {
          alert('提交成功!, 刚才提交的内容是：' + response.body.content)
        },
        (response) => {
          alert('出错了')
        }
        )
    },
    change_title: function () {
      this.title = '修改成功'
    }
  },
  components: {
    MyLogo
  }
}
</script>

<style>
</style>
