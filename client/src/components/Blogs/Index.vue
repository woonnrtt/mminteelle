<template>
<div>
<h2>ระบบจัดการสินค้าออนไลน์</h2>

<h4>จำนวน สินค้า {{blogs.length}}</h4>
<p><button v-on:click="navigateTo('/blog/create')">เพิ่มสินค้า</button></p>
<div v-for="blog in blogs" v-bind:key="blog.id">
<p>id สินค้า: {{ blog.id }}</p>
<p>ชื่อสินค้า: {{ blog.title }}</p>
<p>รายละเอียด: {{ blog.content }}</p>
<p>ราคา: {{ blog.category }}</p>
<p>status: {{ blog.status }}</p>
<p>
<button v-on:click="navigateTo('/blog/'+ blog.id)">ดูข้อมูลสินค้า</button>
<button v-on:click="navigateTo('/blog/edit/'+ blog.id)">แก้ไขสินค้า</button>
<button v-on:click="deleteBlog(blog)">ลบข้อมูล</button>
</p>
<hr>
</div>
</div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
data () {
return {
blogs: []
}
},
async created () {
this.blogs = (await BlogsService.index()).data
},
methods: {

navigateTo (route) {
this.$router.push(route)
},
async deleteBlog (blog) {
let result = confirm("Want to delete?")
if (result) {
try {
await BlogsService.delete(blog)
this.refreshData()
} catch (err) {
console.log(err)
}
}
},
async refreshData() {
this.blogs = (await BlogsService.index()).data
}
}
}
</script>
<style scoped>
</style>