<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <AppHeader />
    <div>
        <div class="Videocover">
            <img :src=list.poster alt="">
        </div>
        <div class="title">
            <p>{{ list.videoTitle }}</p>
            <div>
                <div class="videoinformation">
                    <span>{{ list.author }}</span>
                    <div class="videodata">
                        <div class="towatch">
                            <span>41.4万</span><span>观看</span>
                        </div>
                        <span class="towatch">41.4万</span>
                        <span class="towatch">41.4万</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <VideoBottom />
</template>

<script setup lang="ts">
import AppHeader from '@/components/app-header.vue'
import axios from 'axios'
import { ref } from 'vue'
import { useRoute } from 'vue-router'
import VideoBottom from './components/video-bottom.vue'
const route = useRoute()
interface IVideoInfo {
    id: number
    videoSrc: string
    poster: string
    videoTitle: string
    author: string
    authorIconSrc: string
    playCount: string
    likeCount: string
    favCount: string
    commentCount: 1345,
    date: string
}
const list = ref<IVideoInfo[]>([])
axios({
  method: 'get',
  url: '/videoDetail',
  params: { id: route.params.id }
}).then(res => {
  console.log('视频列表数据', res.data.result)
  list.value = res.data.result
})

</script>

<style scoped lang="less">
.Videocover {
    img {
        width: 100%
    }
}

.title {
    p {
        padding: 10px 10px;
    }

    .videoinformation {
        font-size: 10px;
    }

    .videodata {
        color: rgb(156, 156, 156);
    }

    .videoinformation {
        display: flex;
        justify-content: space-between;

        span {
            margin: 0 8px;
        }

        .videodata {
            display: flex;

            .towatch {
                margin: 0 8px;
            }
        }
    }
}
</style>
