<template>
<div>
<h1>แก้ไขรายละเอียดสินค้า</h1>
<form v-on:submit.prevent = "editBlog">
<p>ชื่อสินค้า: <input type="text" v-model="blog.title"></p>
<p>รายละเอียด: <input type="text" v-model="blog.content"></p>
<p>ราคา: <input type="text" v-model="blog.category"></p>
<p>status: <input type="text" v-model="blog.status"></p>
<p>
<button type="submit">update</button>
<button v-on:click="navigateTo('/blogs')">กลับ </button>
</p>
</form>
</div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
data () {
return {
blog: {
title: '',
thumbnail: 'null',
pictures: 'null',
content: '',
category: '',
status: ''
}
}
},
methods: {
async editBlog () {
try {
await BlogsService.put(this.blog)
this.$router.push({
name: 'blogs'
})
} catch (err) {
console.log(err)
}
}
},
async created () {
try {
let blogId = this.$route.params.blogId
this.blog = (await BlogsService.show(blogId)).data
} catch (error) {
console.log (error)
}
}
}
</script>
<style scoped>
</style>