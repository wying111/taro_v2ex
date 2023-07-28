<template>
  <view class="index">
    <thread-list :threads="threads" :loading="loading" />
  </view>
</template>

<script>
import { reactive, onMounted } from 'vue'
import Taro from '@tarojs/taro'
import api from '../../utils/api'
import ThreadList from '../../components/thread_list.vue'
import './index.less'

export default {
  components: {
    'thread-list': ThreadList,
  },
  setup() {
    const loading = reactive(true)
    const threads = reactive([])

    onMounted(async () => {
      try {
        const res = await Taro.request({
          url: api.getLatestTopic(),
        })
        loading.value = false
        threads.value = res.data
      } catch (error) {
        Taro.showToast({
          title: '载入远程数据错误',
        })
      }
    })

    return {
      loading,
      threads,
    }
  }
}
</script>
