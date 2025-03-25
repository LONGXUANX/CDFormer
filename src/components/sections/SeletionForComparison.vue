<script>
export default {
  data() {
    return {
      value1: '',
      value2: '',
      folder1: 'dataset1',
      folder2: 'dataset2',
      baseImagePath: './image_comparison/',
      comparison1ImagePath: '',
      comparison2ImagePath: '',
      comparison1Loading: true,
      comparison2Loading: true,
      options1: ['deepfish', 'NEU-DET', 'UODD', 'DIOR', 'Clipart', 'Artaxor'],
      options2: ['deepfish', 'NEU-DET', 'UODD', 'DIOR', 'Clipart', 'Artaxor'],
      supportedExtensions: ['.png', '.jpg', '.jpeg'] // 支持的图片格式
    }
  },
  beforeMount() {
    this.handleChange1(this.options1[0]);
    this.handleChange2(this.options2[0]);
  },
  methods: {
    async handleChange1(value) {
      await this.loadImage(value, 'folder1');
    },
    async handleChange2(value) {
      await this.loadImage(value, 'folder2');
    },
    async loadImage(value, folderType) {
      const loadingKey = `${folderType}Loading`.replace('folder', 'comparison');
      const pathKey = `${folderType}ImagePath`.replace('folder', 'comparison');
      const folder = this[folderType];
      
      this[loadingKey] = true;
      let foundPath = '';
      
      // 尝试所有支持的扩展名
      for (const ext of this.supportedExtensions) {
        const testPath = `${this.baseImagePath}${folder}/${value}${ext}`;
        try {
          const exists = await this.checkImageExists(testPath);
          if (exists) {
            foundPath = testPath;
            break;
          }
        } catch (error) {
          console.warn(`Test load failed for ${testPath}`);
        }
      }
      
      if (foundPath) {
        const img = new Image();
        img.src = foundPath;
        img.onload = () => {
          this[pathKey] = foundPath;
          this[loadingKey] = false;
        };
        img.onerror = () => {
          console.error(`Failed to load: ${foundPath}`);
          this[loadingKey] = false;
        };
      } else {
        console.error(`No valid image found for ${value} in ${folder}`);
        this[loadingKey] = false;
      }
    },
    checkImageExists(url) {
      return new Promise((resolve) => {
        const img = new Image();
        img.onload = () => resolve(true);
        img.onerror = () => resolve(false);
        img.src = url;
      });
    }
  }
}
</script>

<template>
  <!-- 保持原有的template结构不变 -->
  <div>
    <el-divider />
    <el-row justify="center">
      <h1 class="section-title">Comparison</h1>
    </el-row>
    <!-- ...原有template内容... -->
  </div>
</template>

<style scoped>
/* 保持原有样式不变 */
</style>
