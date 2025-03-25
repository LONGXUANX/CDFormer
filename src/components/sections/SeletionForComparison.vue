<script>
export default {
  data() {
    return {
      value1: '',
      value2: '',
      folder1: 'CD-ViTO',
      folder2: 'CDFormer(Ours)',
      baseImagePath: './image_comparison/',
      comparison1ImagePath: '',
      comparison2ImagePath: '',
      comparison1Loading: true,
      comparison2Loading: true,
      comparison1Error: false, // 新增错误状态
      comparison2Error: false, // 新增错误状态
      options1: ['deepfish', 'NEU-DET', 'UODD', 'DIOR', 'Clipart', 'Artaxor'],
      options2: ['deepfish', 'NEU-DET', 'UODD', 'DIOR', 'Clipart', 'Artaxor'],
      supportedExtensions: ['.png', '.jpg', '.jpeg'],
      placeholderImage: 'data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="200" height="150" viewBox="0 0 200 150"><rect width="100%" height="100%" fill="%23f5f5f5"/><text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" fill="%23999" font-family="Arial">No Image</text></svg>'
    }
  },
  beforeMount() {
    this.handleChange1(this.options1[0]);
    this.handleChange2(this.options2[0]);
  },
  methods: {
    async handleChange1(value) {
      this.comparison1Error = false;
      await this.loadImage(value, 'folder1');
    },
    async handleChange2(value) {
      this.comparison2Error = false;
      await this.loadImage(value, 'folder2');
    },
    async loadImage(value, folderType) {
      const loadingKey = `${folderType}Loading`.replace('folder', 'comparison');
      const pathKey = `${folderType}ImagePath`.replace('folder', 'comparison');
      const errorKey = `${folderType}Error`.replace('folder', 'comparison');
      const folder = this[folderType];
      
      this[loadingKey] = true;
      this[errorKey] = false;
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
          this[errorKey] = true;
          this[pathKey] = this.placeholderImage;
          this[loadingKey] = false;
        };
      } else {
        console.error(`No valid image found for ${value} in ${folder}`);
        this[errorKey] = true;
        this[pathKey] = this.placeholderImage;
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
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Comparison</h1>
    </el-row>

    <el-row justify="center">
      <el-col>
        <el-row justify="center" :gutter="20">
          <!-- 第一个图片区域 -->
          <el-col :xs="12" :sm="10" :md="8" :lg="6" :xl="6">
            <div class="demo-image">
              <div class="block">
                <el-skeleton
                  style="width: 100%"
                  :loading="comparison1Loading"
                  animated
                  :throttle="1000"
                >
                  <template #template>
                    <el-skeleton-item variant="image" style="width: 100%; height: 100%" />
                  </template>
                  <template #default>
                    <div class="image-container">
                      <el-image 
                        :src="comparison1ImagePath || placeholderImage" 
                        style="width: 100%; height: 100%" 
                        fit="scale-down"
                      >
                        <template #error>
                          <div class="image-error">
                            <el-icon><warning /></el-icon>
                            <span>Failed to load image</span>
                          </div>
                        </template>
                      </el-image>
                      <div v-if="comparison1Error" class="image-status error">Not Found</div>
                    </div>
                  </template>
                </el-skeleton>
                <span class="demonstration">input: {{ comparison1ImagePath || 'No data' }}</span>
              </div>
            </div>

            <el-row justify="center">
              <el-select
                class="select"
                v-model="value1"
                placeholder="Select Dataset 1"
                size="large"
                @change="handleChange1"
              >
                <el-option
                  v-for="item in options1"
                  :key="item"
                  :label="item"
                  :value="item"
                />
              </el-select>
            </el-row>
          </el-col>

          <!-- 第二个图片区域 -->
          <el-col :xs="12" :sm="10" :md="8" :lg="6" :xl="6">
            <div class="demo-image">
              <div class="block">
                <el-skeleton
                  style="width: 100%"
                  :loading="comparison2Loading"
                  animated
                  :throttle="1000"
                >
                  <template #template>
                    <el-skeleton-item variant="image" style="width: 100%; height: 100%" />
                  </template>
                  <template #default>
                    <div class="image-container">
                      <el-image 
                        :src="comparison2ImagePath || placeholderImage" 
                        style="width: 100%; height: 100%" 
                        fit="scale-down"
                      >
                        <template #error>
                          <div class="image-error">
                            <el-icon><warning /></el-icon>
                            <span>Failed to load image</span>
                          </div>
                        </template>
                      </el-image>
                      <div v-if="comparison2Error" class="image-status error">Not Found</div>
                    </div>
                  </template>
                </el-skeleton>
                <span class="demonstration">input: {{ comparison2ImagePath || 'No data' }}</span>
              </div>
            </div>

            <el-row justify="center">
              <el-select
                class="select"
                v-model="value2"
                placeholder="Select Dataset 2"
                size="large"
                @change="handleChange2"
              >
                <el-option
                  v-for="item in options2"
                  :key="item"
                  :label="item"
                  :value="item"
                />
              </el-select>
            </el-row>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.select {
  padding-top: 10px;
  width: 200px;
}

.demo-image .block {
  padding: 20px 0 0 0;
  text-align: center;
  border-right: solid 1px var(--el-border-color);
  display: inline-block;
  width: 100%;
  box-sizing: border-box;
  vertical-align: top;
  position: relative;
}

.demo-image .block:last-child {
  border-right: none;
}

.demo-image .demonstration {
  padding-top: 10px;
  display: block;
  color: var(--el-text-color-secondary);
  word-wrap: break-word;
}

.image-container {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 150px;
}

.image-error {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  color: #f56c6c;
}

.image-status {
  position: absolute;
  bottom: 10px;
  right: 10px;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 12px;
}

.image-status.error {
  background-color: #fef0f0;
  color: #f56c6c;
  border: 1px solid #fde2e2;
}
</style>
