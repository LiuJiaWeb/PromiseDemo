<template>
  <div class="container">


  </div>
</template>



<script setup>
import { onMounted } from 'vue';


/**
 * @description: 获取列表
 */
const getList = () => {
  const promise = new Promise((resolve, reject) => {
    fetch(`${window.location.origin}/src/mock/list.json`)
    .then(response => response.json())
    .then(data => resolve(data))
  })
  return promise
}


/**
 * @description: 获取详情
 */
const getDetail = (id) => {
  const promise = new Promise((resolve, reject) => {
    if(!id) reject('没有id')
    fetch(`${window.location.origin}/src/mock/detail.json`)
      .then(response => response.json())
      .then(data => {
        const target = data.find(it => +it.id === +id)
        if (!target) reject('没有找到对应详情')
        resolve(target)
      })
  })
  return promise
}


onMounted(async () => {
  const list = await getList()
  const detail = await getDetail(list[0].id)
  console.log(detail)
})


</script>

<style lang="less" scoped>
.container{
  width: 100%;
  height: 100vh;
  background-color: #dcdcdc;
  padding: 50px 20px;
}

</style>