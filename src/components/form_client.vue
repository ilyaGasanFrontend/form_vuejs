<!-- Родительский компонент -->
<template>
    <div class="wrapper_form">
        <h1 class="title_form">Form</h1>
        <form action="" class="from_block" @submit.prevent="submitHandler">
            <!-- Включаем дочерний компонент только при условии current_page === 1 -->
            <f_form_component v-if="current_page === 1" :set_attr_f_page="set_attr_f_page" />
            <s_form_component v-if="current_page === 2" :set_attr_s_page="set_attr_s_page"></s_form_component>
            <t_form_component v-if="current_page === 3" :set_attr_s_page="set_attr_s_page"></t_form_component>
            
        </form>
    </div>
</template>

<script>
import { ref } from "vue";
import header_component from "./Header_component.vue"
import f_form_component from "./F_form_component.vue";
import s_form_component from "./S_form_component.vue";
import t_form_component from "./T_form_component.vue";


export default {
    components: {
        f_form_component,
        s_form_component,
        t_form_component,
        header_component

    },
    data() {
        return {
            
            list_selected_group: new Set(),
            current_page: 1,
            form_data : {
                phone_number: 1, // Исправлено на phone_number
                name: ref(''),
                second_name: ref(''),
                patronymic: ref(''),
                gender: ref(''),
                date: ref(''),
                doctor: ref(''),
                message: ref(''),
                
                index: ref(''),
                contry: ref(''),
                area: ref(''),
                city: ref(''),
                street: ref(''),
                house: ref(''),
            }
            
        };
    },
    methods: {
        set_attr_f_page(data) {
            this.form_data.list_selected_group = data.list_selected_group;
            this.form_data.phone_number = data.phone_number;
            this.form_data.name = data.name;
            this.form_data.second_name = data.second_name;
            this.form_data.patronymic = data.patronymic;
            this.form_data.gender = data.gender;
            this.form_data.date = data.date;
            this.form_data.doctor = data.doctor;
            this.form_data.message = data.message;
            this.current_page++
        },
        set_attr_s_page(data) {
            this.form_data.index= data.index,
            this.form_data.contry= data.contry,
            this.form_data.area= data.area,
            this.form_data.city= data.city,
            this.form_data.street= data.street,
            this.form_data.house= data.house,
            this.current_page++
        }
    }
};
</script>

<style scoped></style>