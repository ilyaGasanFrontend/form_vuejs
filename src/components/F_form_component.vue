<template>
    <div class="grope_column">
        <div class="groupe_row groupe_row_mrb">
            <div class="groupe_input">

                <label>Фамилия</label>
                <input placeholder="Фамилия" id="user_name" v-model="second_name" type="text" class="text_input_atrr">
                <span class="error"> {{ errors.second_name_error }}</span>

            </div>
            <div class="groupe_input">

                <label>Имя</label>
                <input placeholder="Имя" id="user_secondname" v-model="name" type="text" class="text_input_atrr">
                <span class="error"> {{ errors.name_error }}</span>

            </div>
        </div>
        <div class="groupe_row groupe_row_mrb ">

            <div class="groupe_input">
                <label>Отчество</label>
                <input placeholder="Отчество" id="patronymic" v-model="patronymic" type="text" class="text_input_atrr">
                <span class="error"> {{ errors.patronymic_error }}</span>

            </div>
            <div class="groupe_input">
                <label class="date_label">Дата рождения</label>
                <input type="date" v-model="date" class="text_input_atrr">
                <span class="error"> {{ errors.date_error }}</span>

            </div>
        </div>
    </div>


    <div class="groupe_row groupe_row_mrb">
        <div class="groupe_input">
            <label>Номер телефона</label>
            <input placeholder="+79217010075" v-model="phone_number"  type="text"
            class="text_input_atrr text_input_phone">
            <span class="error"> {{ errors.phone_number_error }}</span>

        </div>
        <div class="groupe_input ">
            <label>Пол</label>
            <div class="radio_group">
                <label><input type="radio" name="gender" value="m" v-model="gender"> Муж.</label>
                <label><input type="radio"  name="gender" value="w" v-model="gender"> Жен.</label>
            </div>
            <span class="error"> {{ errors.gender_error }}</span>

        </div>
    </div>
    <div class="groupe_row groupe_row_mrb">
        <div class="groupe_input groupe_input--width">
            <a @click="openModal" class="border-button">Выбрать группы</a>
            <div class="container_selected_items">
                <div class="list_selected_items">
                    <item_selector v-for="el in selected_items" @click="deleteElement(el.name)" :key="el.name"
                        :name="el.name"></item_selector>
                </div>
            </div>
            <span class="error"> {{ errors.selected_items_error }}</span>

        </div>
    </div>
    <div class="groupe_row groupe_row_mrb">
        <div class="groupe_input ">
            <label>Выберите лечещего доктора</label>
            <select class="selector" v-model="doctor" name="" id="">
                <option class="selector_option" value="nil" disabled selected>Выберите вашего лечещегро врача
                </option>
                <option class="selector_option" value="1">1</option>
                <option class="selector_option" value="2">2</option>
                <option class="selector_option" value="3">3</option>
            </select>
            <span class="error"> {{ errors.doctor_error }}</span>
        </div>
    </div>
    <div class="groupe_row groupe_row_mrb">
        <div class="groupe_input flex_start">
            <input type="checkbox" class="custom-checkbox" v-model="message" id="happy" name="happy" value="yes">
            <label>Happy</label>
        </div>
    </div>
    <ModalWindow v-if="showModal" :showModal="showModal" @close="closeModal()" :list_el="list_selcted_items"
        @select="addItem"></ModalWindow>
    <a @click="return_attrs" type="submit" class="border-button">Button</a>
</template>

<script>
import { ref } from 'vue'; // Импортируем функцию ref из Vue
import item_selector from "./selecor_item.vue";
import ModalWindow from "./ModalWindow.vue";

export default {
    components: {
        item_selector,
        ModalWindow
    },
    data() {
        return {
            list_selcted_items: [{ id:0, name: 'VIP' }, {id:1, name: 'Проблемные' }, {id:2, name: 'ОМС' }],
            showModal: false,
            phone_number: '', // Исправлено на phone_number
            selected_items: new Set(),
            name: ref(''),
            second_name: ref(''),
            patronymic: ref(''),
            gender: ref(''),
            date: ref(''),
            doctor: ref(''),
            message: ref(''),
            errors: {
                phone_number_error: '',
                selected_items_error: '',
                name_error: '',
                second_name_error: '',
                patronymic_error: '',
                gender_error: '',
                date_error: '',
                doctor_error: '',
            }
        };
    },
    props: ['set_attr_f_page'],
    methods: {
        check_forms() {
            if (this.selected_items.size < 1) {
                this.errors.selected_items_error = 'Выберите хотябы одну группу'
                return false
            }
            this.errors.selected_items_error = ''
            if (this.name.length < 1) {
                this.errors.name_error = 'Имя дожно быть длиннее одного символа'
                return false
            }
            this.errors.name_error = ' '

            if (this.second_name.length < 1) {
                this.errors.second_name_error = 'Фамилия дожна быть длиннее одного символа'
                return false
            }
            this.errors.second_name_error = ' '

            if (this.phone_number.toString().length != 11) {
                console.log(this.phone_number.toString().length)
                this.errors.phone_number_error = 'Номер должен состоять из 11 символов'
                return false
            } else if (this.phone_number.toString()[0] != '8') {
                console.log(this.phone_number.toString()[0])

                this.errors.phone_number_error = 'Номер должен начинаться с цифры 8'
                return false
            }
            this.errors.phone_number_error = 'Номер должен состоять из 11 символов'

           
            this.errors.date_error = ''

            return true

        },
        deleteElement(name) {
            for (const item of this.selected_items) {
                if (item.name === name) {
                    this.selected_items.delete(item);
                    break; // После удаления элемента можно выйти из цикла
                }
            }
        },
        openModal() {
            this.showModal = true;
        },
        closeModal() {
            this.showModal = false;
        },
        addItem(names) {
            for (let i = 0; i < names.length; i++) {
                const name = names[i];
                if (!this.isNameInSelectedItems(name)) {
                    this.selected_items.add({ name: name });
                }
            }
            this.showModal = false; // Закрыть модальное окно после выбора элемента
        },
        isNameInSelectedItems(name) {
            for (const item of this.selected_items) {
                if (item.name === name) {
                    return true;
                }
            }
            return false;
        },
        return_attrs() {
            if (this.check_forms()) {
                let data = {
                    list_selected_group: this.selected_items,
                    phone_number: this.phone_number,
                    name: this.name,
                    second_name: this.second_name,
                    patronymic: this.patronymic,
                    gender: this.gender,
                    date: this.date,
                    doctor: this.doctor,
                    message: this.message
                };

                // Вызовите метод set_attr_f_page и передайте ему объект data
                if (typeof this.set_attr_f_page === 'function') {
                    this.set_attr_f_page(data);
                } else {
                    console.error('Функция set_attr_f_page не определена или не является функцией');
                }
            }

        }
    }
};
</script>

<style scoped></style>