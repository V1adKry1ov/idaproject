<template>
    <div class="create-form">
        <div class="input-div">
            <p class="form-input-text form-input-text--required">Наименование товара</p>
            <input type="text" :class="['form-input', isNameProductValide ? '' : 'form-input--invalide']" placeholder="Введите наименование товара" v-model="nameProduct">
            <p v-if="!isNameProductValide" class='primary-text'>Поле является обязательным</p>
        </div>
        <div class="input-div">
            <p class="form-input-text">Описание товара</p>
            <textarea class="form-textarea" placeholder="Введите описание товара" v-model="descProduct"></textarea>
        </div>
        <div class="input-div">
            <p class="form-input-text form-input-text--required">Ссылка на изображение товара</p>
            <input type="text" :class="['form-input', isImgProductValide ? '' : 'form-input--invalide']" placeholder="Введите ссылку" v-model="imgProduct">
            <p v-if="!isImgProductValide" class='primary-text'>Поле является обязательным</p>
        </div>
        <div class="input-div">
            <p class="form-input-text form-input-text--required">Цена товара</p>
            <input type="text" :class="['form-input', isPriceProductValide ? '' : 'form-input--invalide']" placeholder="Введите цену" v-model="maskPrice"
                @focus="changePrice = true"
                @blur="changePrice = false"
            >
            <p v-if="!isPriceProductValide" class='primary-text'>Поле является обязательным</p>
        </div>
        <button :class="['add-button', isValideForm ? 'add-button--active' : 'add-button--disable']" @click="addProduct">Добавить товар</button>
    </div>
</template>
<script>

export default {
  name: 'CreateForm',
  data() {
      return {
          nameProduct: '',
          isNameProductValide: true,

          descProduct: '',

          imgProduct: '',
          isImgProductValide: true,

          priceProduct: '',
          isPriceProductValide: true,
          changePrice: false
      }
  },
  methods: {
      addProduct() {
          this.nameProduct.length > 0 ? this.isNameProductValide = true : this.isNameProductValide = false;
          this.imgProduct.length > 0 ? this.isImgProductValide = true : this.isImgProductValide = false;
          this.priceProduct ? this.isPriceProductValide = true : this.isPriceProductValide = false;

          if(this.isValideForm) {
              const product = {
                  id: Math.random(),
                  name: this.nameProduct,
                  desc: this.descProduct,
                  img: this.imgProduct,
                  price: this.priceProduct
              }
              this.$emit('add-product', product)
              this.nameProduct = '';
              this.descProduct = '';
              this.imgProduct = '';
              this.priceProduct = '';
          }
      }
  },
  computed: {
      isValideForm() {
          return this.nameProduct.length > 0 && this.imgProduct.length > 0 && this.priceProduct ? true : false
      },
      maskPrice: {
          get() {
              return this.changePrice ? this.priceProduct : this.priceProduct.toLocaleString('ru-RU');
          },
          set(value) {
              this.priceProduct = +value.replace(/\s/g, "")
              if(value === '') {
                  this.priceProduct = ''
              }
              this.$emit('input', this.priceProduct)
          }
      }
  }
}
</script>

<style lang="scss" scoped>
@use "src/consts/colors" as colors;
.create-form {
    position: fixed;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1.5rem;
    background: colors.$white-primary;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    min-width: 20.75rem;
}
.input-div {
    display: flex;
    flex-direction: column;
    gap: .25rem    
    
}
.form-input-text {
    color: colors.$black-secondary;
    font-size: .625rem;
    line-height: 0.8125rem;
    &--required::after {
        color: colors.$red-primary;
        content: " *";
    }
}
.form-input {
    padding: 0.625rem 1rem .625rem 1rem;
    background: colors.$white-primary;
    border: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    font-family: 'Source Sans Pro', sans-serif;
    font-size: 0.75rem;
    line-height: 0.9375rem;
    transition: all .25s cubic-bezier(.02,.01,.47,1);

    &:hover {
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.4);
    }

    &--invalide {
        border: 1px solid colors.$red-primary;
    }
}
.form-textarea {
    padding: 0.625rem 1rem .625rem 1rem;
    background: colors.$white-primary;
    border: none;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    resize: none;
    height: 6.75rem;
    box-sizing: border-box;
    font-family: 'Source Sans Pro', sans-serif;
    font-size: 0.75rem;
    line-height: 0.9375rem;
    transition: all .25s cubic-bezier(.02,.01,.47,1);

    &:hover {
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.4);
    }
}

.primary-text {
    font-size: .5rem;
    line-height: .625rem;
    color: colors.$red-primary;
}

.add-button {
    border-radius: 10px;
    font-weight: 600;
    font-size: .75rem;
    line-height: .9375rem;
    padding: .625rem 0;
    border: none;
    


    &--active {
        background: colors.$green-primary;
        color: #fff;
    }

    &--disable {
        background: colors.$grey-bg;
        color: colors.$grey-primary;
    }
}
@media screen and (max-width: 800px) {
  .create-form {
      position: static;
  }
}
</style>