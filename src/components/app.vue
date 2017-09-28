<template>
    <div id="WBAQPage" class="WBAQPage">
        <carousel :slides="slides" :inv="invTime"></carousel>
    </div>
</template>
<script>
import carousel from './Carousel'
export default {
    data() {
        return {
            invTime: 2000,
            slides: [
                { url: 'http://echarts.baidu.com/echarts2/doc/asset/img/slide-01.png', link: '#' },
                { url: 'http://echarts.baidu.com/echarts2/doc/asset/img/slide-02.png', link: '#' },
                { url: 'http://echarts.baidu.com/echarts2/doc/asset/img/slide-03.png', link: '#' },
                { url: 'http://echarts.baidu.com/echarts2/doc/asset/img/slide-04.png', link: '#' },
                { url: 'http://echarts.baidu.com/echarts2/doc/asset/img/slide-05.jpg', link: '#' }
            ]
        }
    },
    components:{
        carousel
    }
}
</script>
<<style scoped>

</style>


