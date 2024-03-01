<template>
    <div class="registerForm">
        <h2>Заполните форму</h2>
        <form  @submit.prevent="submitForm" class="form">
            <div class="form__item">
                <input id="postalCode" v-model="postalCode" />
                <label for="postalCode">Индекс</label>
            </div>
            <div class="form__item">
                <input id="country" v-model="country" />
                <label for="country">Страна</label>
            </div>
            <div class="form__item">
                <input id="region" v-model="region" />
                <label for="region">Область</label>
            </div>
            <div class="form__item">
                <p v-if="$v.city.$error" class="form__error">Город обязателен</p>
                <input id="city" v-model="city" :class="{'is-invalid': $v.city.$error}" />
                <label for="city">Город</label>
            </div>
            <div class="form__item">
                <input id="street" v-model="street" />
                <label for="street">Улица</label>
            </div>
            <div class="form__item">
                <input id="house" v-model="house" />
                <label for="house">Дом</label>
            </div>
            <button class="registerForm__continue"> Далее</button>
        </form>
    </div>
  </template>
  
  <script>
  import { required } from 'vuelidate/lib/validators'
  import { validationMixin } from 'vuelidate'
  
  export default {
    mixins: [validationMixin],
    data() {
      return {
        postalCode: '',
        country: '',
        region: '',
        city: '',
        street: '',
        house: '',
      }
    },
    validations: {
      city: { required },
    },
    methods: {
        submitForm() {
        this.$v.$touch()
        if (!this.$v.$invalid) {
            const formData = {
                postalCode: this.postalCode,
                country: this.country,
                region: this.region,
                city: this.city,
                street: this.street,
                house: this.house
            };
            this.$emit('set-data',formData)
        }
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
.registerForm {
    background: white;
    padding: 40px 100px;
    border-radius: 20px;
    box-shadow: 0 4px 6px rgba(0.1, 0.1, 0.1, 0.1); 
    &__continue {
        background: #6d8be4;
        color: white;
        padding: 12px 30px;
        font-family: 'Roboto';
        margin-top: 24px;
        border-radius: 8px;
        border: 0;
        cursor: pointer;
        width: 100px;
    }
    .form {
        display: flex;
        flex-direction: column;
        gap: 16px;
        .form__row {
            display: flex;
            flex-direction: row !important;
        }
        .form__item {
            width: 400px;
            display: flex;
            flex-direction: column-reverse;
            text-align: left;
            gap: 4px;
            .form__error {
                color: red;
                font-size: 12px;
                margin-top: 2px;
                margin-left: 8px;
            }
            label {
                font-size: 16px;
                color: #2d3748;
            }
            input {
                padding: 8px 12px;
                border:1px solid #e2e8f0;
                border-radius: 4px;
                &:focus {
                    outline: none;
                    border: 1px solid #31333b;
                }
            }
            input[type='date'] {
                width: 100px;
            }
            
            .field {
                padding: 8px 12px;
                border:1px solid #e2e8f0;
                border-radius: 4px;
                &:focus {
                    outline: none;
                    border: 1px solid #6d8be4;
                }
            }
        }
}
}
@media (max-width:500px) {
    .registerForm {
        padding: 10px;

        .form {
            align-items: center;
            .form__item {
                width: 280px;
            }
        }
    }
}
  </style>