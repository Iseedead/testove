<template>
  <div class="content">
    <span>{{ label }}</span>
    <div>
      <div class="mediaWrapper" v-for="media in medias">
        <div class="pretty p-default" @click="show">
          <input v-model="media.isChecked" :cheked="media.isChecked" type="checkbox"/>
          <div class="state">
            <label>{{media.media}}</label>
          </div>
        </div>
        <div class="mediaDataWrapper">
          <transition name="slide-fade">
            <input :class="media.valid"
                   v-model.trim="media.value"
                   v-if="media.isChecked"
                   :placeholder="media.media"
                   type="text"
            />
          </transition>
        </div>
      </div>
    </div>
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
        information: {},
        label: '3. Отметьте социальные сети',
        medias: [
          {
            media: 'Facebook',
            value: this.userInfo.Facebook,
            isChecked: this.userInfo.Facebook !== '',
            valid: ''
          },
          {
            media: 'Вконтакте',
            value: this.userInfo.Вконтакте,
            isChecked: this.userInfo.Вконтакте !== '',
            valid: ''
          },
          {
            media: 'Twitter',
            value: this.userInfo.Twitter,
            isChecked: this.userInfo.Twitter !== '',
            valid: ''
          },
          {
            media: 'Одноклассники',
            value: this.userInfo.Одноклассники,
            isChecked: this.userInfo.Одноклассники !== '',
            valid: ''
          }
        ],
        btns: [
          {
            prev: 'Предыдущий',
            next: 'Следующий',
          }
        ]
      }
    },
    methods: {
      getNext() {
        let i = 0;
        this.medias.forEach(media => {
          if (media.isChecked === true) {
            i++;
            if (media.value === '') {
              media.valid = 'notValid';
            } else {
              media.valid = '';
              this.information[media.media] = media.value;
            }
          }
        });
        if (Object.keys(this.information).length === i) {
          this.$emit('getNext', this.information);
        }
      },
      getPrev() {
        this.$emit('getPrev');
      },
      show() {
        this.medias.forEach(media => {
          if (media.isChecked === false) {
            media.valid = '';
            media.value = '';
          }
        });
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

  .mediaWrapper {
    padding: 10px 0 0 0;
  }

  input[type="text"] {
    font-family: "Open Sans", sans-serif;
    padding: 3px;
    border: 0;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    border-radius: 2px;
  }

  input[type="text"]::placeholder {
    font-family: "Open Sans", sans-serif;
    color: #bbbbbb;
  }

  .mediaDataWrapper {
    display: inline-block;
    position: absolute;
    margin: -3px 0 0 0;
  }

  input[type="text"].notValid {
    border: 1px solid #ff0000;
  }

</style>
