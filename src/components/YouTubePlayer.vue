<script>
import { store } from '../store'
export default{
    name: 'YouTubePlayer',
    data() {
        return {
            store,
        }
    },
}


</script>

<template>
    <section id="yt-player" class="my-5">
    <div class="container">
        <div class="row">
            <!-- video grande -->
            <div class="col-8 px-0 text-end">
                <!-- video 1 -->
                 <div class="">
                    <iframe width="880" height="550" :src="store.videoArray[store.activeVideo].video" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
                 </div>
            </div>
            <!-- sexione lista video -->
            <div id="video-list" class="col-4 px-0">
                <!-- header lista video -->
                <div id="player-header" class="col-12 d-flex align-items-center player-card">
                    <div class="col-2 p-3 text-center">
                        <i class="fa-solid fa-play"></i>
                    </div>
                    <div class="col-10">
                        <h6 class="mb-0">Video Playlist</h6>
                        <span> {{ store.videoArray[store.activeVideo].id }}/{{ store.videoArray.length }} </span>
                    </div>                    
                </div>
                <!-- body lista player -->
                <div id="player-body" class="overflow-y-auto">
                    <!-- card video -->
                    <div class="col-12 d-flex align-items-center player-card clickable" v-for="(video, index) in store.videoArray" :key="video.id" @click="store.activeVideo = index" :class="{ active: store.activeVideo === index }">
                        <!-- numero video -->
                        <div class="col-1">
                            <div class="vd-number text-center ms-1">
                                <span v-if="store.activeVideo === index"><i class="fa-solid fa-play"></i></span>
                                <span v-else>{{ video.id }}</span>
                            </div>
                        </div>
                        <!-- thumbnail video -->
                         <div class="col-3 vd-thumb">
                            <img :src="video.thumb" :alt="video.title">
                         </div>
                         <!-- titolo video -->
                          <div class="col-8 vd-title">
                            <span>{{ video.title }}</span>
                          </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>
</template>

<style lang="scss" scoped>
@use '../style/partials/variables' as *;

#yt-player{    
    .player-card{
        height: 100px;
        background-color: $tertiary-color;
        border-bottom: 1px solid $quaternary-color;
        &:hover{
                color: $primary-color;

                .vd-number{
                    background-color: $primary-color;
                }
            }


        &:last-child{
            border-bottom: none;
        }

        .vd-number{
            background-color: $quaternary-color;
            color: white;
            border-radius: 5px;
            height: 30px;
            width: 30px;
            line-height: 28px;
        }

        .vd-thumb{
            img{
                width: 80%;
                border-radius: 15px;
                margin: 0 10px;
            }
        }
    }
    #player-header{
        height: 90px;
        background-color: $quaternary-color;
        color: white;

        i{
            font-size: 40px;
        }
        span{
            font-size: 13px;
        }
    }

    #player-body{
        height: 460px;

        .active{
            color: $primary-color;

            .vd-number{
                background-color: $primary-color;
            }
        }
    }
}


</style>