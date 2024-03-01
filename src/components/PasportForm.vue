<template>
    <div class="registerForm">
        <h2>Заполните форму</h2>
        <form @submit.prevent="submitForm" class="form">
            <div class="form__item">
                <span v-if="$v.documentType.$error" class="form__error">Тип документа обязателен</span>
                <select class="field" id="documentType" v-model="$v.documentType.$model" :class="{'is-invalid': $v.documentType.$error}">
                    <option disabled value="">Выберите тип</option>
                    <option>Паспорт</option>
                    <option>Свидетельство о рождении</option>
                    <option>Водительское удостоверение</option>
                </select>
                <label for="documentType">Тип документа</label>
            </div>
            <div class="form__item">
                <input id="series" v-model="series" />
                <label for="series">Серия</label>
            </div>
            <div class="form__item">
                <input id="number" v-model="$v.number.$model" :class="{'is-invalid': $v.number.$error}" />
                <label for="number">Номер</label>
            </div>
            <div class="form__item">
                <input id="issuedBy" v-model="issuedBy" />
                <label for="issuedBy">Кем выдан</label>
            </div>
            <div class="form__item">
                <span v-if="$v.issueDate.$error" class="form__error">Дата выдачи обязательна</span>
                <input type="date" id="issueDate" v-model="$v.issueDate.$model" :class="{'is-invalid': $v.issueDate.$error}" />
                <label for="issueDate">Дата выдачи</label>
            </div>

            <button class="registerForm__continue"> Далее</button>
        </form>

    </div>
</template>
  
<script>
    import { required  } from 'vuelidate/lib/validators'
    import { validationMixin } from 'vuelidate'
  
  export default {
    mixins: [validationMixin],
    data() {
    return {
      documentType: '',
      series: '',
      number: '',
      issuedBy: '',
      issueDate: '',
    }
  },
  validations: {
    documentType: { required },
    number: {},
    issueDate: { required },
  },
    methods: {
      submitForm() {
        this.$v.$touch()
        if (!this.$v.$invalid) {
            const formData = {
            documentType: this.documentType,
            series: this.series,
            number: this.number,
            issuedBy: this.issuedBy,
            issueDate: this.issueDate,
            }
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