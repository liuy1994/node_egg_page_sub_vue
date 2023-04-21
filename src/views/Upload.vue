<script setup lang="ts">
import { getCurrentInstance, onMounted, ref } from "vue"
const input = ref<any>(null)
const getUrl = ref<any>(null)

const onChange = () => {
  const file = input?.value?.files?.[0]
  const blobUrl = URL.createObjectURL(file);
  getUrl.value?.(blobUrl)
}

onMounted(() => {
  const $qiankun = getCurrentInstance()!.appContext.app.config.globalProperties.$qiankun
  getUrl.value = $qiankun.getUrl
})

</script>

<template>
  <div>
    <input type="file" @change="onChange" ref="input" accept="image/png, image/jpeg">
  </div>
</template>

<style scoped lang="less">
input {
  font-size: 16px;
}
img {
  width: 32px;
  object-fit: contain;
}
</style>
