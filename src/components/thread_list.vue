<template>
    <view className="thread-list">
        <loading v-if="loading" />
        <thread v-else v-for="t in threads" :key="t.id" :node="t.node" :title="t.title" :last_modified="t.last_modified"
            :replies="t.replies" :tid="t.id" :member="t.member" />
    </view>
</template>
  
<script>
import { defineProps } from 'vue'
import Loading from './loading.vue'
import Thread from './thread.vue'

export default {
    components: {
        Loading,
        Thread,
    },
    setup() {
        const props = defineProps({
            threads: {
                type: Array,
                default: () => [],
            },
            loading: {
                type: Boolean,
                default: true,
            },
        })

        return {
            ...props,
        }
    },
}
</script>