<template>
  <div class="content">
    <div class="info">
      <div class="name">
        <span>{{ userInfo.name }}</span>
      </div>
      <div class="mail">
        <span>{{ userInfo.mail }}</span>
      </div>
      <div class="address">
        <span>{{ userInfo.city }}, {{ userInfo.country }}</span>
      </div>
      <div class="media">
        <span v-if="userInfo.Facebook !== ''"><a>Facebook: </a>{{ userInfo.Facebook }}</span>
        <span v-if="userInfo.Twitter !== ''"><a>Twitter: </a>{{ userInfo.Twitter }}</span>
        <span v-if="userInfo.Вконтакте !== ''"><a>Вконтакте: </a>{{ userInfo.Вконтакте }}</span>
        <span v-if="userInfo.Одноклассники !== ''"><a>Одноклассники: </a>{{ userInfo.Одноклассники }}</span>
      </div>
    </div>
    <div class="avatar">
      <img :src="userInfo.image" width="200px" height="195px"/>
    </div>
    <Btn
      v-for="btn in btns"
      :key="btn.id"
      :btn="btn"
      @getNext="getNext"
    >
    </Btn>
  </div>
</template>

<script>
  import Btn from './Btn.vue'

  export default {
    components: {
      Btn
    },
    props: [
      'userInfo'
    ],
    data() {
      return {
        btns: [
          {
            next: 'Пройти заново',
            nextClass: 'finish',
            prevClass: 'off'
          }
        ]
      }
    },
    methods: {
      getNext() {
        this.$emit('getNext');
      }
    }
  }
</script>

<style scoped>
  .content {
    width: 550px;
    height: 243px;
    background: #ffffff;
    display: inline-flex;
    border-radius: 2px;
    margin: 35px 0 0 -160px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
  }

  .content .buttonWrapper {
    margin: 275px 0 0 210px;
    position: absolute;
  }

  .avatar {
    margin: 24px 0;
  }

  .avatar img {
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
  }

  .info {
    width: 326px;
  }

  .name {
    margin: 24px 0 0 25px;
    font-size: 20px;
  }

  .mail {
    margin: 12px 0 0 25px;
  }

  .address {
    margin: 16px 0 0 25px;
  }

  .media {
    margin: 30px 0 0 25px;
    display: inline-grid;
  }

  .media a {
    color: #2849ad;
  }
</style>
