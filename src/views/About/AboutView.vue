<template>
  <div class="about-background min-h-screen">
    <HeroComponent
      title="关于我们"
      sub-title="说明文本"
      background-url="/cpdc-platform/exhibition/5.png"
      title-color="white"
    />

    <main class="mx-auto w-full max-w-5xl px-4 py-8 md:px-8 md:py-12">
      <section class="rounded-xl bg-white/90 p-5 shadow-md backdrop-blur-sm md:p-8">
        <h2 class="text-primary mb-4 text-2xl font-bold">项目说明</h2>
        <p class="text-secondary-700 whitespace-pre-wrap leading-8">
          {{ descriptionText }}
        </p>
      </section>
    </main>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import HeroComponent from '@/components/Hero/HeroComponent.vue'

const descriptionText = ref('正在加载说明内容...')

const loadDescription = async () => {
  try {
    const response = await fetch(`${import.meta.env.BASE_URL}shuoming.txt`)
    if (!response.ok) {
      throw new Error('加载说明文本失败')
    }
    descriptionText.value = await response.text()
  } catch (error) {
    console.error(error)
    descriptionText.value = '说明文本加载失败，请稍后重试。'
  }
}

onMounted(() => {
  loadDescription()
})
</script>

<style scoped>
.about-background {
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0.7)),
    url('/cpdc-platform/herobg.png');
  background-position: center;
  background-size: cover;
}
</style>
