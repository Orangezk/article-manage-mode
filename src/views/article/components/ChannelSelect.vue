<script setup>
import { artGetChannelService } from '@/api/article'
import { ref } from 'vue'

defineProps({
  modelValue: {
    type: [String, Number]
  }
})
const emit = defineEmits(['update:modelValue'])
const channelList = ref()
const getChannelList = async () => {
  const res = await artGetChannelService()
  channelList.value = res.data.data
}
getChannelList()
</script>

<template>
  <el-select
    style="width: 240px"
    :modelValue="modelValue"
    @update:modelValue="emit('update:modelValue', $event)"
  >
    <el-option
      v-for="channel in channelList"
      :key="channel.id"
      :label="channel.cate_name"
      :value="channel.id"
    ></el-option>
  </el-select>
</template>
