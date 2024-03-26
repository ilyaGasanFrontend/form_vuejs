<template>
    
    <div class="grope_column">
        <div class="groupe_row">
            <div class="groupe_input">
                <label>Индекс</label>
                <input placeholder="Индекс" v-model="index" type="text" class="text_input_atrr">
            </div>
            <div class="groupe_input">
                <label>Страна</label>
                <input placeholder="Страна" v-model="contry" type="text" class="text_input_atrr">
            </div>
        </div>
        <div class="groupe_row">
            <div class="groupe_input">
                <label>Область</label>
                <input placeholder="Область" v-model="area" type="text" class="text_input_atrr">
            </div>
            <div class="groupe_input">
                <label>Город</label>
                <input placeholder="Город" v-model="city" type="text" class="text_input_atrr">
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
export default {
    data() {
        return {
            index: '',
            contry: '',
            area: '',
            city: '',
            street: '',
            house: '',
        }
    },
    props: ['set_attr_s_page'],
    methods: {
        send_attr_s() {
            let data = {
                index: this.index,
                contry: this.contry,
                area: this.area,
                city: this.city,
                street: this.street,
                house: this.house,
            }
            if (typeof this.set_attr_s_page === 'function') {
                this.set_attr_s_page(data);
            } 
        }
    }
}
</script>

<style scoped>
</style>
