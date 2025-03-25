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
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Comparison</h1>
    </el-row>

    <el-row justify="center">
      <el-col >
        <el-row justify="center" :gutter="20">

          <el-col :xs="12" :sm="10" :md="8" :lg="6" :xl="6" >

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
                    <el-image :src="comparison1ImageRootPath" style="width: 100%; height: 100%" fit="scale-down"/>
                  </template>
                </el-skeleton>
                <span class="demonstration">input: {{ comparison1ImageRootPath }}</span>
              </div>
            </div>

            <el-row justify="center">
                <el-select
                  class="select"
                  v-model="value1"
                  placeholder="Select"
                  size="large"
                  @change="handleChange1"
                >
                  <el-option
                    v-for="item in options"
                    :key="item"
                    :label="item"
                    :value="item"/>
                </el-select>
            </el-row>

          </el-col>

          <el-col :xs="12" :sm="10" :md="8" :lg="6" :xl="6" >
            
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
                    <el-image :src="comparison2ImageRootPath" style="width: 100%; height: 100%" fit="scale-down"/>
                  </template>
                </el-skeleton>
                <span class="demonstration">input: {{ comparison2ImageRootPath }}</span>
              </div>
            </div>

            <el-row justify="center">
              <el-select
                class="select"
                v-model="value2"
                placeholder="Select"
                size="large"
                @change="handleChange2"
              >
                <el-option
                  v-for="item in options"
                  :key="item"
                  :label="item"
                  :value="item"/>
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

/* 路径文字居中 */
.demo-image .block {
  padding: 20px 0 0 0;
  text-align: center;
  border-right: solid 1px var(--el-border-color);
  display: inline-block;
  width: 100%;
  box-sizing: border-box;
  vertical-align: top;
}

.demo-image .block:last-child {
  border-right: none;
}

/* 路径文字颜色 */
.demo-image .demonstration {
  padding-top: 10px;
  display: block;
  color: var(--el-text-color-secondary);
  word-wrap: break-word;
}

</style>
