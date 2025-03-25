<script lang="ts">
import { defineComponent } from 'vue'
import resultsTable from './image_comparison/CDFormer.bmp' // 替换为你的图片路径

export default defineComponent({
  data() {
    return {
      tableImage: resultsTable,
      imageAlt: '实验对比结果表格（mAP值）' // 替换为你的图片描述
    }
  }
})
</script>

<template>
  <div class="table-container">
    <img 
      :src="tableImage" 
      :alt="imageAlt"
      class="responsive-table"
    >
  </div>
</template>

<style scoped>
.table-container {
  margin: 0 auto;
  max-width: 900px; /* 根据你的图片宽度调整 */
  padding: 20px;
}

.responsive-table {
  width: 100%;
  height: auto;
  display: block;
  border: 1px solid #eee;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

/* 移动端适配 */
@media (max-width: 768px) {
  .table-container {
    padding: 10px;
  }
}
</style>
