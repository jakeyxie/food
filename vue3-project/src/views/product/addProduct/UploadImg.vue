<template>
  <el-upload
    v-model:file-list="props.fileList"
    :action="uploadUrl"
    list-type="picture-card"
    :on-success="success"
    :on-remove="handleRemove"
  >
    <el-icon><Plus /></el-icon>
  </el-upload>

</template>

<script setup>
import { ref } from 'vue'
import { Plus } from '@element-plus/icons-vue'
import  { UploadProps, UploadUserFile } from 'element-plus'
import {uploadUrl,host} from '@/api/product'
const emit= defineEmits(['sendImgUrl'])
const props = defineProps(['fileList'])

// const fileList = ref([
// //   {
// //     name: 'food.jpeg',
// //     url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
// //   },
// ])


const handleRemove = (uploadFile, uploadFiles) => {
  console.log(uploadFile, uploadFiles)
}

const success = (response) => {
  console.log('response',response);
  //需要获取正确的网址 访问这个图片  发送给添加商品接口 img地址
    let url = host+'/'+ response.url.slice(7)
    console.log(url);
    emit('sendImgUrl',url)
}
</script>

<style>

</style>