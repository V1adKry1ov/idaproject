<template>
  <div class="wrapper">
    <div class="header-wrapper">
      <h1 class="header-wrapper__text">Добавление товара</h1>
      <div :class="['select', isActiveSelect ? 'select--active' : '']">
        <div @click="isActiveSelect = !isActiveSelect" class="select__title">{{selectedValue}}</div>
        <div v-if="isActiveSelect" class="select__content">
          <input id="minSelect" class="select__input" type="radio" @click="changeSelect('По возрастанию')"/>
          <label for="minSelect" class="select__label" >По возрастанию</label>
          <input id="maxSelect" class="select__input" type="radio" @click="changeSelect('По убыванию')"/>
          <label for="maxSelect" class="select__label">По убыванию</label>
          <input id="nameSelect" class="select__input" type="radio" @click="changeSelect('По алфавиту')"/>
          <label for="nameSelect" class="select__label">По алфавиту</label>
        </div>
      </div>
    </div>
    <div class="body-wrapper">
      <create-form class="create-form" @add-product="addProduct"/>
      <div class="products">
          <product-el v-for="(product, index) in products" :key="product.id" :product="product" @delete-product="deleteProduct(index)"/>
      </div>
    </div>
  </div>
</template>

<script>
import CreateForm from '@/components/CreateForm.vue'
import Product from '@/components/Product.vue'

export default {
  name: 'App',
  components: {
    'create-form': CreateForm,
    'product-el': Product
  },
  data() {
    return {
      products: [],
      initialProducts: [
        {
          id: Math.random(),
          img: 'https://i.pinimg.com/550x/5b/52/a0/5b52a0667e4a6082d476e9b65f5c82d3.jpg',
          name: 'Я Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          id: Math.random(),
          img: 'https://handcraftguide.com/sites/default/files/styles/original___water/public/sketchingforkids4handcraftguide.com_.jpg?itok=I2Q9q-2e',
          name: 'ПНаименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 110000
        },
        {
          id: Math.random(),
          img: 'https://www.iguides.ru/upload/medialibrary/9f8/9f8fdff471b7d281f81f694c100b5adc.png',
          name: 'Ы Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 800
        },
        {
          id: Math.random(),
          img: 'https://img.kapital.kz/H-Nb-9q3EjU/czM6Ly9rYXBpdGFsLXN0YXRpYy9pbWcvOS8xLzQvMS9kL2JjNjk4MmMwNDQ3NDQxZTIxY2FhMDBkNWI3Zi5qcGc',
          name: 'В Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000000
        },
        {
          id: Math.random(),
          img: 'https://www.iphones.ru/wp-content/uploads/2021/05/NyanCat.jpg',
          name: 'А Наименование товара',
          desc: 'Довольно-таки интересное описание товара ',
          price: 120
        },
        {
          id: Math.random(),
          img: 'http://sun9-27.userapi.com/sun9-81/s/v1/if1/zO5oA6Nt-lyk_mEjEBH6ZJFSg4-xMggN9oiad_4UG317hI8rrDYNu0fNPHbXsymcIlKr5ADD.jpg?size=200x219&quality=96&crop=20,0,420,460&ava=1',
          name: 'З Наименование товара',
          desc: '',
          price: 120123
        }
      ],
      isActiveSelect: false,
      selectedValue: 'По умолчанию'
      
    }
  },
  created() {
    if(localStorage.getItem('products') === null) {
      this.products = this.initialProducts
    } else {
      this.products = JSON.parse(localStorage.getItem('products'));
    }
  },
  methods: {
    addProduct(value) {
      this.products.push(value)
      localStorage.setItem("products",JSON.stringify(this.products));
    },
    deleteProduct(index) {
      this.products.splice(index, 1);
      localStorage.setItem("products",JSON.stringify(this.products));
    },
    changeSelect(value) {
      this.selectedValue = value;
      this.isActiveSelect = false;

      if(value === 'По возрастанию') {
        this.products.sort((a, b) => {
          return a.price - b.price
        })
      }
      else if (value === 'По убыванию') {
        this.products.sort((a, b) => {
          return b.price - a.price
        })
      }
      else if (value === 'По алфавиту') {
        this.products.sort((a, b) => {
          return a.name.localeCompare(b.name)
        })
      }
    }
  },
}
</script>

<style lang="scss">
@use "src/consts/colors" as colors;
body {
  background: colors.$body-bg;
}

.wrapper {
  padding: 2rem;
}

.header-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;

  &__text {
    font-weight: 600;
    font-size: 1.75rem;
    line-height: 2.1875rem;
    color: colors.$black-primary;
  }
}
.body-wrapper {
  display: flex;
  align-items: flex-start; 
  gap: 1rem;
}

.products {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-left: 25rem;
}

.select {
  position: relative;
  width: 10rem;
  &--active {
    .select__title {
      &::before {
        transform: translate(-1px, -50%) rotate(-45deg);
      }

      &::after {
        transform: translate(1px, -50%) rotate(45deg);
      }
    }
    
    .select__content {
      opacity: 1;
    }
    
    .select__label + .select__input + .select__label {
      border-top-width: 1px;
    }
  }
}
.select__title {
  display: flex;
  align-items: center;
  padding: 10px 26px 11px 16px;

  background: colors.$white-primary;
  font-size: .75rem;
  line-height: 0.9375rem;
  color: colors.$grey-primary;

  border-radius: 5px;
  border: solid 1px colors.$grey-primary;
  
  cursor: pointer;

  &::before,
  &::after {
    content: "";

    position: absolute;
    top: 20px;
    right: 8px;

    display: block;
    width: 5px;
    height: 2px;

    transition: all 0.3s ease-out;

    background-color: colors.$grey-primary;

    transform: translate(-1px, -50%) rotate(45deg);
  }
  &::after {
    transform: translate(1px, -50%) rotate(-45deg);
  }

  &:hover {
    border-color: colors.$black-primary;

    &::before,
    &::after {
      background-color: colors.$black-primary;
    }
  }
}

.select__content {
  position: absolute;
  top: 38px;
  left: 3px;

  display: flex;
  flex-direction: column;


  background-color: colors.$white-primary;

  border: 1px solid colors.$white-primary;
  border-top: none;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  
  transition: all 0.3s ease-out;

  opacity: 0;
  z-index: 8;
}
.select__input {
  display: none;

  &:checked + label {
    background-color: colors.$white-primary;
  }
  &:disabled + label {
    opacity: 0.6;
    pointer-events: none;
  }
}
.select__label {
  display: flex;
  align-items: center;
  background: colors.$white-primary;
  font-size: .75rem;
  line-height: 0.9375rem;
  color: colors.$grey-primary;
  width: 7.5rem;
  padding: 10px 12px 11px 16px;
  
  transition: all 0.2s ease-out;

  cursor: pointer;
  
  overflow: hidden;

  & + input + & {
    border-top: 0 solid #C7CCD160;
  }

  &:hover {
    background-color: colors.$green-primary !important;

    color: colors.$white-primary;
  }
}

@media screen and (max-width: 800px) {
  .body-wrapper {
    flex-direction: column;
  }
  .products {
    margin-left: 0;
  }
}
</style>
