<template>
    <form @submit.prevent="submitForm" class="form">
        <div class="form__item">
            <p v-if="$v.firstName.$error" class="form__error">Это поле обязательна</p>
            <input v-model.trim="$v.firstName.$model" type="text" id="firstname">
            <label for="firstname">Имя</label>
        </div>
        <div class="form__item">
            <p v-if="$v.lastName.$error" class="form__error">Это поле обязательна</p>
            <input  v-model.trim="$v.lastName.$model"  type="text" id="lastname">
            <label for="lastname">Фамилия</label>
        </div>
        <div class="form__item">
            <input id="patronymic" v-model.trim="$v.patronymic.$model" />
            <label for="patronymic">Отчество</label>
        </div>
        <div class="form__item">
            <p v-if="$v.birthDate.$error" class="form__error">Дата рождения обязательна</p>
            <input type="date" id="birthDate" v-model.trim="$v.birthDate.$model" :class="{'is-invalid': $v.birthDate.$error}" />
            <label for="birthDate">Дата рождения</label>
        </div>
        <div class="form__item">
            <p v-if="$v.phoneNumber.$error" class="form__error">Номер телефона обязателен и должен содержать 11 цифр</p>
            <input id="phoneNumber" v-model.trim="$v.phoneNumber.$model" :class="{'is-invalid': $v.phoneNumber.$error}" />
            <label for="phoneNumber">Номер телефона</label>
        </div>
        <div class="form__item">
            <select class="field" id="gender" v-model.trim="$v.gender.$model">
                <option value=""></option>
                <option value="male">Мужской</option>
                <option value="female">Женский</option>
            </select>
            <label for="gender">Пол</label>
        </div>   
        <div class="form__item">
            <p v-if="$v.customerGroup.$error" class="form__error">Выберите хотя бы одну группу клиентов</p>
            <select class="field" multiple v-model.trim="$v.customerGroup.$model" :class="{'is-invalid': $v.customerGroup.$error}">
                <option value="VIP">VIP</option>
                <option value="problem">Проблемные</option>
                <option value="OMS">ОМС</option>
            </select>
            <label>Группа клиентов1</label>
        </div>
        <div class="form__item">
            <p v-if="$v.attendingDoctor.$error" class="form__error">Выберите лечащего врача</p>
            <select class="field" id="attendingDoctor" v-model.trim="$v.attendingDoctor.$model" :class="{'is-invalid': $v.attendingDoctor.$error}">
                <option value=""></option>
                <option value="Иванов">Иванов</option>
                <option value="Захаров">Захаров</option>
                <option value="Чернышева">Чернышева</option>
            </select>
            <label>Лечащий врач</label>
        </div>
        <div class="form__item form__row">
            <label for="dontSendSms">Не отправлять Смс</label>
            <input type="checkbox" id="dontSendSms" v-model.trim="$v.dontSendSms.$model" />
        </div>
        <button class="form__continue"> Далее</button>
    </form>
</template>

<script>
  import { required, 
    minLength, maxLength, numeric
} from 'vuelidate/lib/validators';
  import { validationMixin } from 'vuelidate';

    export default {
        mixins: [validationMixin],
        data() {
            return {
            firstName:'',
            lastName:'',
            patronymic:'',
            birthDate:'',
            phoneNumber:'',
            gender:'',
            customerGroup:[],
            attendingDoctor:'',
            dontSendSms: false
            }
        },
        validations: {
            firstName: {
                required
            },
            lastName: {
                required
            },
        patronymic: {},
        birthDate: {
            required
        },
        phoneNumber: {
            required,
            minLength: minLength(11),
            maxLength: maxLength(11),
            numeric
        },
        gender: {},
        customerGroup: {
            required
        },
        attendingDoctor: {
            required
        },
        dontSendSms: {

        }
        },
        methods: {
        submitForm() {  
            this.$v.$touch()
            if (!this.$v.$invalid) {
                const formData = {
                    firstName: this.firstName,
                    lastName: this.lastName,
                    patronymic: this.patronymic,
                    birthDate: this.birthDate,
                    phoneNumber: this.phoneNumber,
                    gender: this.gender,
                    customerGroup: this.customerGroup,
                    attendingDoctor: this.attendingDoctor,
                    dontSendSms: this.dontSendSms
                };
                this.$emit('set-data',formData)
            }
      }
    }
    }
</script>

<style lang="scss" scoped>
    .form__continue {
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
        align-items: center;
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


@media (max-width:500px) {
        .form {
            align-items: center;
            .form__item {
                width: 280px;
            }
        }
}
</style>