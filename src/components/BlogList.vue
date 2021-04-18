<template>
  <div >
    <table>
      <tr v-for="blog in blogs" :key="blog.index">
        <td @click='show_blog(blog.id)'>{{blog.title }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: '博客列表项',
      blogs: [
      ]
    }
  },
  mounted () {
    this.$http.get('api/interface/blogs/all').then((response) => {
      console.info(response.body)
      this.blogs = response.body.blogs
    }, (response) => {
      console.error(response)
    })
  },
  methods: {
    show_blog: function (blogId) {
      this.$router.push({name: 'Blog', query: {id: blogId}})
    }
  }
}
</script>

<style >
td {
  border-bottom: 1px solid grey;
}
</style>
