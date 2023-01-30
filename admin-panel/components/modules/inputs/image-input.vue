<template>
  <div class="image-input-wrapper">
    <p class="title">{{ title }}</p>
    <label for="file-input" class="file-label">
      <input
        @change="getImages"
        id="file-input"
        class="file-input"
        type="file"
        multiple="multiple"
      />
      <div class="image-preview" v-if="imageUrls && imageUrls.length > 0">
        <img :src="imageUrls[currentIndex]" />
      </div>
      <div class="image-controllers" v-if="this.imageUrls.length >= 2">
        <button @click="previousImage" class="previous image-controller">
          <IconPrevious />
        </button>
        <button @click="nextImage" class="next image-controller">
          <IconNext />
        </button>
      </div>
      <div
        class="image-delete-container"
        v-if="imageUrls && imageUrls.length > 0"
      >
        <button class="delete-image" @click="deleteImage(currentIndex)">
          <IconDelete />
        </button>
      </div>
    </label>
  </div>
</template>

<script>
export default {
  //! some adjustments needs to be done with this component
  //! all depends on the project the it is used on
  props: {
    title: {
      type: String,
      default: 'image',
    },
  },
  data() {
    return {
      imageUrls: [],
      currentIndex: 0,
    };
  },
  components: {
    IconPrevious: () => import('@/components/icons/icon-previous.vue'),
    IconNext: () => import('@/components/icons/icon-next.vue'),
    IconDelete: () => import('@/components/icons/icon-delete.vue'),
  },
  methods: {
    getImages(e) {
      const imageFiles = e.target.files;
      for (let i = 0; i < imageFiles.length; i++) {
        const imageFile = imageFiles[i];
        const imageUrl = URL.createObjectURL(imageFile);
        this.imageUrls.push(imageUrl);
        this.currentIndex = this.imageUrls.length - 1;
      }
    },
    nextImage() {
      if (this.currentIndex === this.imageUrls.length - 1) {
        this.currentIndex = 0;
      } else {
        this.currentIndex = this.currentIndex + 1;
      }
    },
    previousImage() {
      if (this.currentIndex === 0) {
        this.currentIndex = this.imageUrls.length - 1;
      } else {
        this.currentIndex = this.currentIndex - 1;
      }
    },
    deleteImage(index) {
      this.imageUrls.splice(index, 1);
      this.currentIndex = index - 1;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.image-input-wrapper {
  width: 100%;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
}
.title {
  margin-bottom: 10px;
  font-size: 16px;
  font-weight: 300;
}
.image-preview {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%;
  height: 100%;
  position: absolute;

  img {
    width: 100%;
    height: 100%;
    border-radius: 10px;
  }
}
.image-controllers {
  position: absolute;
  z-index: 2;
  top: calc(50% - 15px);
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 5px;
}
.image-delete-container {
  position: absolute;
  z-index: 2;
  top: 10px;
  right: 10px;
}
.delete-image {
  cursor: pointer;
  background-color: $eton-blue;
  border: none;
  border-radius: 2px;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  svg {
    width: 20px;
    height: 22px;
    fill: $white;
  }
}
.image-controller {
  width: 30px;
  height: 30px;
  background-color: $eton-blue;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  svg {
    width: 100%;
    height: 100%;
    fill: $white;
  }
}
.file-label {
  position: relative;
  width: 340px;
  height: 170px;
  cursor: pointer;
  border: 2px solid $eton-blue;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  background-color: $bright-gray;
  background-image: url('@/static/images/index.png');
  border-radius: 10px;
}
.file-input {
  display: none;
}
</style>
