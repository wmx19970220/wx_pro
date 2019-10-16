<template>
  <div>
    <div v-for = "item in data" :key = "item">
      <div>{{  item.name }}</div>
      <img  :src = "item.url"  />
      <button @click= "col(item)"> 收藏 </button>
    </div>
    <div @click= "collection">前往收藏页面</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      data:[]
    }
  },
  mounted(){
    let url = 'http://10.31.153.29:1216/data.json'
    wx.request({
      url,
      success: res => {
        this.data = res.data
      }
    })
  },
  methods:{
    col(item){
      let myBooks = wx.getStorageSync('myBooks') || []
      let flag = myBooks.some(items => items.name == item.name)
      flag || myBooks.push(item)
      wx.setStorageSync('myBooks',myBooks)
    },
    collection(){
      wx.navigateTo({
        
      })
    }
  }
}
</script>

<style scoped>

</style>
