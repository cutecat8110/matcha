<template>
  <section class="common-section-padding bg-system-dark text-white">
    <div class="container relative flex flex-col gap-y-10 lg:px-[5.75rem]">
      <!-- 背景裝飾．竹狀 -->
      <SvgBamboo class="bamboo-r" />

      <!-- 標題 -->
      <div class="flex items-end gap-4">
        <h2 class="section-title">最新</h2>
        <p class="section-sub-title text-system-main-400">News</p>
      </div>

      <!--  desktop．輪播 -->
      <Swiper
        class="relative hidden w-full overflow-visible md:block"
        :modules="[Navigation]"
        :navigation="{ nextEl: '.nextEl', prevEl: '.prevEl' }"
        :slides-per-view="slidesView"
        :space-between="40"
        data-aos="fade-left"
      >
        <SwiperSlide v-for="(news, index) in newsList" :key="index">
          <NewsCard :news="news" />
        </SwiperSlide>

        <!--  輪播控制器 -->
        <UiButton class="prevEl" state="icon">
          <SvgArrow class="rotate-180" />
        </UiButton>
        <UiButton class="nextEl" state="icon">
          <SvgArrow />
        </UiButton>
      </Swiper>

      <!--  mobile．輪播 -->
      <div class="flex flex-col gap-y-6 md:hidden">
        <NewsCard
          v-for="(news, index) in newsList.slice(0, 2)"
          :key="index"
          :news="news"
          data-aos="fade"
        />
      </div>

      <!--  連結．最新消息頁 -->
      <div class="flex flex-row-reverse">
        <router-link to="/">
          <UiButton state="outline" tag="span">
            view all
            <template #trailing>
              <SvgArrow />
            </template>
          </UiButton>
        </router-link>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import SvgArrow from '@/components/svg/SvgArrow.vue'
import { useWindowSize } from '@vueuse/core'
import { Navigation } from 'swiper/modules'
import NewsCard from './NewsCard.vue'

const newsList = ref([
  {
    type: '線上',
    src: '/maccha/img/news01.jpg',
    alt: '',
    date: '2024.06.01',
    content: '2024年夏季中元禮品特輯已公開！【官方線上商店】'
  },
  {
    type: '線上',
    src: '/maccha/img/news02.jpg',
    alt: '',
    date: '2024.06.01',
    content: '2024年父親節禮品已公開！【官方線上商店】'
  },
  {
    type: '新品',
    src: '/maccha/img/news03.jpg',
    alt: '',

    date: '2024.06.01',
    content: '甜祇園 × MACCHA 合作甜點第一彈「宇治抹茶奶油夾心餅乾 巧妙堆疊」將於4月20日開始銷售'
  },
  {
    type: '預購',
    src: '/maccha/img/news04.jpg',
    alt: '',
    date: '2024.06.01',
    content: 'MACCHA 會員限定月替甜點第3彈『宇治抹茶奶油泡芙』現已開放預訂。'
  }
])

/* 輪播 RWD 數量 */
const { width } = useWindowSize()
const slidesView = computed(() => {
  return width.value > 992 ? 3 : 2
})
</script>

<style lang="scss" scoped>
.prevEl,
.nextEl {
  @apply absolute top-1/2 z-[1] -translate-y-1/2 text-system-gray-600 transition-colors duration-500 hover:text-white;

  &.swiper-button-disabled {
    @apply text-system-gray-600;
  }
}
.prevEl {
  @apply left-0 -translate-x-full;
}

.nextEl {
  @apply right-0 translate-x-full;
}
</style>
