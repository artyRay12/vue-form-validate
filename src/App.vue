<template>
    <div id="app" class="form-wrapper">
        <div v-if="submitted" class="success-alert">
            <p class="alert-text">Nice!</p>
            <button class="alert-button" @click="submitted = false">create new</button>
        </div>
        <form class="form" @submit.prevent="onSubmit" v-if="!submitted">
            <div class="main-info">
                <p class="form-group-title">Основная информация</p>
                <div class="input-wrapper">
                    <label
                        for="surname"
                        class="form-label"
                        :class="{'error-text': $v.surname.$error}"
                    >
                        Фамилия
                        <span class="red-text">*</span>
                    </label>
                    <input
                        class="required-input"
                        :class="{'error': $v.surname.$error}"
                        type="text"
                        id="surname"
                        placeholder="Фамилия"
                        @blur="$v.surname.$touch()"
                        v-model="surname"
                    />
                    <div
                        class="error-text"
                        v-if="!$v.surname.required && $v.surname.$dirty"
                    >Введите фамилию</div>
                </div>

                <div class="input-wrapper">
                    <label for="name" class="form-label" :class="{'error-text': $v.name.$error}">
                        Имя
                        <span class="red-text">*</span>
                    </label>
                    <input
                        type="text"
                        id="name"
                        placeholder="Имя"
                        class="required-input"
                        :class="{'error': $v.name.$error}"
                        @blur="$v.name.$touch()"
                        v-model="name"
                    />
                    <div class="error-text" v-if="!$v.name.required && $v.name.$dirty">Введите имя</div>
                </div>

                <div class="input-wrapper">
                    <label for="patronymic" class="form-label">Отчество</label>
                    <input type="text" id="patronymic" placeholder="Отчество" v-model="patronymic" />
                </div>

                <div class="input-wrapper">
                    <label
                        for="birthDay"
                        class="form-label"
                        :class="{'error-text': $v.birthDay.$error}"
                    >
                        Дата рождения
                        <span class="red-text">*</span>
                    </label>
                    <input
                        class="required-input"
                        type="date"
                        id="birthDay"
                        name="birthDay"
                        :class="{'error': $v.birthDay.$error}"
                        @blur="$v.birthDay.$touch()"
                        v-model="birthDay"
                    />
                    <div
                        class="error-text"
                        v-if="!$v.birthDay.required && $v.birthDay.$dirty"
                    >Введите дату рождения</div>
                </div>

                <div class="input-wrapper">
                    <label
                        class="form-label"
                        for="phoneNumber"
                        :class="{'error-text': $v.phoneNumber.$error}"
                    >
                        Номер Телефона
                        <span class="red-text">*</span>
                    </label>
                    <input
                        id="phoneNumber"
                        type="tel"
                        name="phoneNumber"
                        @blur="$v.phoneNumber.$touch()"
                        v-model="phoneNumber"
                        :class="{'error': (!$v.phoneNumber.normalLength || !$v.phoneNumber.required || !$v.phoneNumber.numeric ) 
                                      && $v.phoneNumber.$dirty}"
                    />
                    <div
                        class="error-text"
                        v-if="!$v.phoneNumber.required && $v.phoneNumber.$dirty"
                    >Введите номер телефона</div>
                    <div
                        class="error-text"
                        v-if="!$v.phoneNumber.numeric"
                    >Номер телефона состоит только из цифр</div>

                    <div
                        class="error-text"
                        v-if="!$v.phoneNumber.normalLength && $v.phoneNumber.$dirty"
                    >Номер должен состоять из 11 цифр</div>
                </div>

                <div class="radio-wrapper">
                    <label class="form-label">Пол</label>
                    <p class="radio-input-label">
                        <input
                            name="sex"
                            type="radio"
                            value="male"
                            checked
                            class="sex-input"
                            v-model="sex"
                        /> Мужской
                    </p>
                    <p class="radio-input-label">
                        <input
                            name="sex"
                            type="radio"
                            value="female"
                            class="sex-input"
                            v-model="sex"
                        /> Женский
                    </p>
                </div>

                <div class="selector-wrapper">
                    <div class="client-group-wrapper">
                        <label class="form-label" :class="{'error-text': $v.clientGroup.$error}">
                            Группа клиентов
                            <span class="red-text">*</span>
                        </label>
                        <div class="selectors">
                            <p class="radio-input-label">
                                <input
                                    name="client-group"
                                    type="checkbox"
                                    value="vip"
                                    v-model="clientGroup"
                                    @change="$v.clientGroup.$touch()"
                                /> VIP
                            </p>
                            <p class="radio-input-label">
                                <input
                                    name="client-group"
                                    type="checkbox"
                                    value="problem"
                                    v-model="clientGroup"
                                    @change="$v.clientGroup.$touch()"
                                /> Проблемные
                            </p>
                            <p class="radio-input-label">
                                <input
                                    name="client-group"
                                    type="checkbox"
                                    value="OMC"
                                    v-model="clientGroup"
                                    @change="$v.clientGroup.$touch()"
                                /> ОМС
                            </p>
                        </div>
                    </div>

                    <div
                        class="error-text"
                        v-if="clientGroup.length == 0 && $v.clientGroup.$dirty"
                    >Выберите свою группу клиента</div>
                </div>

                <div class="input-wrapper">
                    <label class="form-label" for="doctors">Лечащий врач</label>
                    <select class="form-select" name="doctors" id="doctors">
                        <option value="Ivanov">Иванов</option>
                        <option value="Zaharov">Захаров</option>
                        <option value="Chernysheva">Чернышева</option>
                    </select>
                </div>

                <p class="radio-input-label">
                    <input name="sms-mode" type="checkbox" value="enable" v-model="smsMode" /> Не отправлять смс
                </p>
            </div>

            <hr />

            <div class="adress-wrapper form-part">
                <p class="form-group-title">Адрес</p>
                <div class="input-wrapper">
                    <label class="form-label" for="index">Индекс</label>
                    <input type="text" id="index" name="index" v-model="index" />
                </div>
                <div class="input-wrapper">
                    <label for="country" class="form-label">Страна</label>
                    <input type="text" id="country" name="country" v-model="country" />
                </div>
                <div class="input-wrapper">
                    <label for="region" class="form-label">Область</label>
                    <input type="text" id="region" name="region" v-model="region" />
                </div>
                <div class="input-wrapper">
                    <label class="form-label" for="city" :class="{'error-text': $v.city.$error}">
                        Город
                        <span class="red-text">*</span>
                    </label>
                    <input
                        type="text"
                        id="city"
                        name="city"
                        v-model="city"
                        @blur="$v.city.$touch()"
                        :class="{'error': !$v.city.required && $v.city.$dirty}"
                    />
                    <div
                        class="error-text"
                        v-if="!$v.city.required && $v.city.$dirty"
                    >Выберите город</div>
                </div>
                <div class="input-wrapper">
                    <label for="street" class="form-label">Улица</label>
                    <input type="text" id="street" name="street" v-model="street" />
                </div>
                <div class="input-wrapper">
                    <label for="house" class="form-label">Дом</label>
                    <input type="text" id="house" name="house" v-model="house" />
                </div>
            </div>

            <hr />

            <div class="passport-wrapper">
                <p class="form-group-title">Документ</p>

                <div class="input-wrapper">
                    <label
                        class="form-label"
                        for="documetType"
                        :class="{'error-text': $v.documentType.$error}"
                    >
                        Тип Документа
                        <span class="red-text">*</span>
                    </label>
                    <select
                        name="documetType"
                        id="documetType"
                        class="form-select"
                        v-model="documentType"
                        @blur="$v.documentType.$touch()"
                        :class="{'error': !$v.documentType.required && $v.documentType.$dirty}"
                    >
                        <option value="passport">Паспорт</option>
                        <option value="birthСertificate">Свидетельство о рождении</option>
                        <option value="driverLicense">Вод. удостоверение</option>
                    </select>
                    <div
                        class="error-text"
                        v-if="!$v.documentType.required && $v.documentType.$dirty"
                    >Выберите документ</div>
                </div>

                <div class="input-wrapper">
                    <label class="form-label" for="series">Серия</label>
                    <input type="text" id="series" name="series" v-model="documentSeries" />
                </div>
                <div class="input-wrapper">
                    <label class="form-label" for="number">Номер</label>
                    <input type="text" id="number" name="number" v-model="documentNumber" />
                </div>
                <div class="input-wrapper">
                    <label class="form-label" for="issuedBy">Кем выдан</label>
                    <input type="text" id="issuedBy" name="issuedBy" v-model="documentIssueBy" />
                </div>
                <div class="input-wrapper">
                    <label
                        class="form-label"
                        for="dateOfIssue"
                        :class="{'error-text': $v.documentIssueDate.$error}"
                    >
                        Дата выдачи
                        <span class="red-text">*</span>
                    </label>
                    <input
                        type="date"
                        id="dateOfIssue"
                        name="dateOfIssue"
                        v-model="documentIssueDate"
                        @blur="$v.documentIssueDate.$touch()"
                        :class="{'error': !$v.documentIssueDate.required && $v.documentIssueDate.$dirty}"
                    />
                    <div
                        class="error-text"
                        v-if="!$v.documentIssueDate.required && $v.documentIssueDate.$dirty"
                    >Введите дату выдачи документа</div>
                </div>
            </div>

            <button type="submit" class="submit-btn" :disabled="$v.$invalid">создать</button>
        </form>
    </div>
</template>

<script>
import { required, numeric } from "vuelidate/lib/validators";

export default {
    name: "app",
    data() {
        return {
            submitted: false,

            surname: null,
            name: null,
            patronymic: null,
            birthDay: null,
            phoneNumber: 7,
            sex: null,
            clientGroup: [],
            smsMode: null,

            index: null,
            country: null,
            region: null,
            city: null,
            street: null,
            house: null,

            documentType: null,
            documentSeries: null,
            documentNumber: null,
            documentIssueBy: null,
            documentIssueDate: null,
        };
    },

    validations: {
        surname: {
            required,
        },
        name: {
            required,
        },
        birthDay: {
            required,
        },
        phoneNumber: {
            required,
            normalLength(phoneNumber) {
                if (String(phoneNumber).length === 11) {
                    return true;
                }
                return false;
            },
            numeric,
        },
        clientGroup: {
            required,
        },
        city: {
            required,
        },
        documentType: {
            required,
        },
        documentIssueDate: {
            required,
        },
    },

    methods: {
        resetForm() {
            this.$v.$reset();
            this.surname = null;
            this.name = null;
            this.patronymic = null;
            this.birthDay = null;
            this.phoneNumber = 7;
            this.sex = null;
            this.clientGroup = [];

            this.index = null;
            this.country = null;
            this.region = null;
            this.city = null;
            this.street = null;
            this.house = null;

            this.documentType = null;
            this.documentSeries = null;
            this.documentIssueBy = null;
            this.documentIssueDate = null;
        },

        onSubmit() {
            this.resetForm();

            this.submitted = true;
        },
    },
};
</script>

<style src="./App.scss" lang="scss">
</style>
