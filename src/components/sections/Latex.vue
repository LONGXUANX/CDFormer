<script lang="ts">
import { defineComponent } from 'vue'
import resultsTable from '/image_comparison/CDFormer.png' // 推荐使用@/assets路径

export default defineComponent({
  data() {
    return {
      tableImage: resultsTable,
      imageAlt: '模型性能对比结果',
      // 新增文本内容
      title: 'Experimental results comparison',
      caption: 'Fig.1 The mAP values of different approaches produced on the CD-FSOD benchmarks in case of 1-shot, 5-shot, and 10-shot. Here ``w/ FT'' and ``w/o FT'' denote the results produced with and without fine-tuning, respectively.'
    }
  }
})
</script>

<template>
  <div class="figure-container">
    <!-- 标题 -->
    <h2 class="figure-title">{{ title }}</h2>
    
    <!-- 图片 -->
    <div class="image-wrapper">
      <img 
        :src="tableImage" 
        :alt="imageAlt"
        class="responsive-image"
        loading="lazy"
      >
    </div>
    
    <!-- 图注 -->
    <p class="figure-caption">{{ caption }}</p>
  </div>
</template>

<style scoped>
.figure-container {
  max-width: 900px;
  margin: 2rem auto;
  text-align: center;
}

.figure-title {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1rem;
  font-weight: 600;
}

.image-wrapper {
  padding: 1rem;
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.1);
  margin: 1rem 0;
}

.responsive-image {
  max-width: 100%;
  height: auto;
  display: block;
  margin: 0 auto;
  border: 1px solid #f0f0f0;
}

.figure-caption {
  font-size: 0.9rem;
  color: #666;
  line-height: 1.6;
  margin-top: 0.5rem;
  font-style: italic;
}

/* 响应式调整 */
@media (max-width: 768px) {
  .figure-container {
    margin: 1rem;
  }
  .figure-title {
    font-size: 1.3rem;
  }
}
</style>
