<template>
  <div class="modal flex">
    <div class="modal-content flex container_elements">

      <div class="wrapper_element" v-for="item in list_el" :key="item" :id="item.id" @click="addItem(item)">
          {{ item.name }}
      </div>
      <a type="button" @click="closeModal()" class="border-button">Добавить</a>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'; // Импортируем функцию ref из Vue
import $ from 'jquery';

export default {
  props: {
    list_el: {
      type: Array,
    },
    showModal: {
      type: Boolean,
      default: false,
    },
  },
  mounted() {
    this.getelelment();
  },
  data() {
    return {
      items_tooadd: [],
      is_active: false,
      list_elements: NaN
    };
  },
  methods: {
    getelelment() {
      this.list_elements = $('.wrapper_element')
      console.log(this.list_elements)
    },
    closeModal() {
      this.$emit('select', this.items_tooadd);
      this.$emit('close');
    },

    addItem(item) {
      console.log(this.items_tooadd.indexOf($(this.list_elements[item.id]).html()))
      let index = this.items_tooadd.indexOf($(this.list_elements[item.id]).html())
      if (index != -1) {
        this.items_tooadd.splice(index,1)
      }
      else{
        this.items_tooadd.push($(this.list_elements[item.id]).html())
      }
      $(this.list_elements[item.id]).toggleClass('is_selected');

    }
  }
};
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  width: 100vw;
  height: 100vh;
  background: #11111167;
  z-index: 100;
}

.flex {
  display: flex;
  justify-content: center;
  align-items: center;
}

.absolute {
  position: relative;
}

.modal-content {
  background: #fff;
  width: 30%;
  height: 50%;
  border-radius: 10px;
  .border-button {
    background: #000;
  }
}

.close {
  position: absolute;
  right: 15px;
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  top: 15px;
  cursor: pointer;
  font-size: 1.2rem;
  background: red;
  border-radius: 50%;

}
.is_selected {
  background: red;
}

</style>