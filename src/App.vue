<template>
    <div id="app" class="form-wrapper">
        <form class="form">
            <div class="main-info">
                <label for="surname">Фамилия</label>
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

                <label for="name">Имя</label>
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

                <label for="patronymic">Отчество</label>
                <input type="text" id="patronymic" placeholder="Отчество" />

                <label for="birthDay" :class="{'error-label': $v.birthDay.$error}">Дата рождения:</label>
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

                <label for="phoneNumber">Номер Телефона</label>
                <input
                    id="phoneNumber"
                    type="tel"
                    name="phoneNumber"
                    value="7"
                    @blur="$v.phoneNumber.$touch()"
                    v-model="phoneNumber"
                    :class="{'error': (!$v.phoneNumber.minLength || !$v.phoneNumber.maxLength
                                     || !$v.phoneNumber.required || !$v.phoneNumber.numeric ) 
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
                <div class="error-text" v-if="!$v.phoneNumber.maxLength">Слишком длинный номер</div>

                <div class="selector-wrapper">
                    <label>Пол</label>
                    <p>
                        <input name="sex" type="radio" value="male" checked /> Мужской
                    </p>
                    <p>
                        <input name="sex" type="radio" value="female" /> Женский
                    </p>
                </div>

                <div class="selector-wrapper">
                    <label>Группа клиентов</label>
                    <p>
                        <input
                            name="client-group"
                            type="checkbox"
                            value="vip"
                            v-model="clientGroup"
                            @change="$v.clientGroup.$touch()"
                        /> VIP
                    </p>
                    <p>
                        <input
                            name="client-group"
                            type="checkbox"
                            value="problem"
                            v-model="clientGroup"
                            @change="$v.clientGroup.$touch()"
                        /> Проблемные
                    </p>
                    <p>
                        <input
                            name="client-group"
                            type="checkbox"
                            value="OMC"
                            v-model="clientGroup"
                            @change="$v.clientGroup.$touch()"
                        /> ОМС
                    </p>
                </div>
                <div
                    class="error-text"
                    v-if="clientGroup.length == 0 && $v.clientGroup.$dirty"
                >Выберите свою группу клиента</div>

                <label for="doctors">Лечащий врач</label>
                <select name="doctors" id="doctors">
                    <option value="Ivanov">Иванов</option>
                    <option value="Zaharov">Захаров</option>
                    <option value="Chernysheva">Чернышева</option>
                </select>

                <p>
                    <input name="sms-mode" type="checkbox" value="enable" /> Не отправлять смс
                </p>
            </div>

            <hr />
            <hr />
            <hr />

            <div class="adress-wrapper">
                <label for="index">Индекс</label>
                <input type="text" id="index" name="index" />

                <label for="country">Страна</label>
                <input type="text" id="country" name="country" />

                <label for="region">Область</label>
                <input type="text" id="region" name="region" />

                <label for="city">Город</label>
                <input
                    type="text"
                    id="city"
                    name="city"
                    v-model="city"
                    @blur="$v.city.$touch()"
                    :class="{'error': !$v.city.required && $v.city.$dirty}"
                />
                <div class="error-text" v-if="!$v.city.required && $v.city.$dirty">Выберите город</div>

                <label for="street">Улица</label>
                <input type="text" id="street" name="street" />

                <label for="house">Дом</label>
                <input type="text" id="house" name="house" />
            </div>

            <hr />
            <hr />
            <hr />

            <div class="passport-wrapper">
                <label for="documetType">Тип Документа</label>
                <select
                    name="documetType"
                    id="documetType"
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
                {{$v.documentType}}
                {{documentType}}
                <label for="series">Серия</label>
                <input type="text" id="series" name="series" />

                <label for="number">Номер</label>
                <input type="text" id="number" name="number" />

                <label for="issuedBy">Кем выдан</label>
                <input type="text" id="issuedBy" name="issuedBy" />

                <label for="street">Улица</label>
                <input type="text" id="street" name="street" />

                <label for="dateOfIssue">Дата выдачи</label>
                <input
                    type="date"
                    id="dateOfIssue"
                    name="dateOfIssue"
                    v-model="issueDate"
                    @blur="$v.issueDate.$touch()"
                    :class="{'error': !$v.issueDate.required && $v.issueDate.$dirty}"
                />
                {{$v.issueDate}}
                <div
                    class="error-text"
                    v-if="!$v.issueDate.required && $v.issueDate.$dirty"
                >Введите дату выдачи документа</div>
            </div>
        </form>
    </div>
</template>

<script>
import {
    required,
    minLength,
    maxLength,
    numeric,
} from "vuelidate/lib/validators";

export default {
    name: "app",
    data() {
        return {
            //         mainInfo: {
            surname: null,
            name: null,
            patronymic: null,
            birthDay: null,
            phoneNumber: null,
            sex: null,
            clientGroup: [],
            //   },

            // adress: {
            index: null,
            country: null,
            region: null,
            city: null,
            street: null,
            house: null,
            // },

            // document: {
            documentType: null,
            siries: null,
            issueBy: null,
            issueDate: null,
            //},
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
            minLength: minLength(11),
            maxLength: maxLength(11),
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
        issueDate: {
            required,
        },
    },
};
</script>

<style src="./App.scss" lang="scss">
</style>
