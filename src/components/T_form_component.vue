<template>
    
    <div class="grope_column">
        <div class="groupe_row groupe_input-doc">
            <div class="groupe_input">

                <select class="selector" v-model="document" name="" id="">
                    <option class="selector_option" value="nil" selected disabled  >Выберите тип документа</option>
                    <option class="selector_option" value="1">1</option>
                    <option class="selector_option" value="2">2</option>
                    <option class="selector_option" value="3">3</option>
                </select>
            </div>
        </div>
        <div class="groupe_row">
            <div class="groupe_input">
                <label>Серия</label>
                <input placeholder="Серия" v-model="series" type="text" class="text_input_atrr">
            </div>
            <div class="groupe_input">
                <label>Номер</label>
                <input placeholder="Номер" v-model="number" type="text" class="text_input_atrr">
            </div>
        </div>
        <div class="groupe_row">
            <div class="groupe_input">
                <label>Кем выдан</label>
                <input placeholder="Кем выдан" v-model="area" type="text" class="text_input_atrr">
            </div>
            <div class="groupe_input">
                <label class="date_label">Дата выдачи</label>
                <input type="date" v-model="date_doc" class="text_input_atrr">
            </div>
        </div>
        <div class="groupe_row">
            <div class="groupe_input">
                <label>Улица</label>
                <input placeholder="Улица" v-model="street" type="text" class="text_input_atrr">
            </div>
            <div class="groupe_input">
                <label>Дом</label>
                <input placeholder="Дом" v-model="house" type="text" class="text_input_atrr">
            </div>
        </div>
    </div>
    <a @click="send_attr_s" class="border-button">Button</a>
</template>

<script>
import { ref } from "vue";

export default {
    data() {
        return {
            doctor: ref(''),
        }
    }
}
</script>

<style>

</style>