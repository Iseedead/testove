<template>
  <div class="content">
    <span>{{ label }}</span>
    <Inputable
      v-for="formable in formables"
      :key="formable.id"
      :formable="formable"
    >
    </Inputable>
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
  import Btn from '../Btn.vue'
  import Inputable from '../Inputable.vue'

  export default {
    components: {
      Btn, Inputable
    },
    data() {
      return {
        information: {},
        label: '1. Введите имя и е-mail',
        formables: [
          {
            value: '',
            title: 'name',
            type: 'text',
            placeholder: 'Имя',
            valid: false,
            error: ' — Неверно введенное имя',
            regex: '^[a-zA-Zа-яА-Я\\s]+$'
          },
          {
            value: '',
            title: 'mail',
            type: 'text',
            placeholder: 'E-mail',
            valid: false,
            error: ' — Неверно введенный почтовый адрес',
            regex: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
          }
        ],
        btns: [
          {
            prev: 'Предыдущий',
            next: 'Следующий',
            prevClass: 'disabled'
          }
        ]
      }
    },
    methods: {
      getNext() {
        this.formables.forEach(form => {
          if (form.value === '' || !form.value.match(form.regex)) {
            form.notValid = 'notValid';
            form.valid = true;
          } else {
            form.notValid = '';
            form.valid = false;
            this.information[form.title] = form.value;
          }
        });
        if (Object.keys(this.information).length === 2) {
          this.$emit('getNext', this.information);
        }
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

</style>
