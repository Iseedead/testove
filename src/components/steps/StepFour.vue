<template>
  <div class="content">
    <span>{{ label }}</span>
    <div class="imageWrapper" v-for="image in images" @click="selectImage(image)">
      <img :class="image.style" :src="image.path" width="150px" height="150px"/>
    </div>
    <span v-if="catValid" class="catError">{{ catError }}</span>
    <Btn
      v-for="btn in btns"
      :key="btn.id"
      :btn="btn"
      @getNext="getNext"
      @getPrev="getPrev"
    >
    </Btn>
  </div>
</template>

<script>
  import Btn from '../Btn.vue'

  export default {
    components: {
      Btn
    },
    props: [
      'userInfo'
    ],
    data() {
      return {
        label: '4. Выберите любимого котика',
        catError: 'Вы выбрали собачку. А надо котика',
        catValid: false,
        btns: [
          {
            prev: 'Предыдущий',
            next: 'Завершить',
            nextClass: 'finish'
          }
        ],
        images: [
          {
            id: 1,
            path: '/src/assets/cat1.jpg',
            style: 'image selected'
          },
          {
            id: 2,
            path: '/src/assets/cat2.jpg',
            style: 'image'
          },
          {
            id: 3,
            path: '/src/assets/cat3.jpg',
            style: 'image'
          },
          {
            id: 4,
            path: '/src/assets/dog4.jpg',
            style: 'image'
          }
        ]
      }
    },
    methods: {
      getNext() {
        this.images.forEach(mage => {
          if (mage.style === 'image selected') {
            if (mage.id === 4) {
              this.catValid = true;
            } else {
              this.$emit('getNext', {image: mage.path});
            }
          }
        });
      },
      getPrev() {
        this.$emit('getPrev');
      },
      selectImage(image) {
        this.images.forEach(mage => {
          mage.style = 'image';
        });
        image.style = 'image selected';
      }
    }
  }
</script>

<style scoped>
  .content {
    margin: 16px auto;
  }

  .content span {
    margin-bottom: 24px;
    display: block;
  }

  .content .buttonWrapper {
    display: block;
    margin: 25px 0 0 0;
  }

  .imageWrapper {
    display: inline-block;
    margin: -1px 16px 0 0;
    animation-name: fadeIn;
    animation-duration: 1s;
  }

  .image {
    border: 0;
    border-radius: 2px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
  }

  .selected {
    border: 3px solid #ff9800;
  }

  span.catError {
    color: #ff0000;
    margin: 16px 0;
  }
</style>
