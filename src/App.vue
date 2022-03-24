<template>
  <div class="wrapper">
    <div class="header-wrapper">
      <h1 class="header-wrapper__text">Добавление товара</h1>
      <p>По умолчанию</p>
    </div>
    <div class="body-wrapper">
      <create-form class="create-form"/>
      <div class="products">
        <product-el v-for="(product, index) in products" :key="index" :product="product"/>
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
      products: [
        {
          img: 'https://i.pinimg.com/550x/5b/52/a0/5b52a0667e4a6082d476e9b65f5c82d3.jpg',
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          img: 'https://handcraftguide.com/sites/default/files/styles/original___water/public/sketchingforkids4handcraftguide.com_.jpg?itok=I2Q9q-2e',
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          img: 'https://mirpozitiva.ru/wp-content/uploads/2019/11/1472042718_14.jpg',
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          img: 'https://img.kapital.kz/H-Nb-9q3EjU/czM6Ly9rYXBpdGFsLXN0YXRpYy9pbWcvOS8xLzQvMS9kL2JjNjk4MmMwNDQ3NDQxZTIxY2FhMDBkNWI3Zi5qcGc',
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          img: 'https://www.iphones.ru/wp-content/uploads/2021/05/NyanCat.jpg',
          name: 'Наименование товара',
          desc: 'Довольно-таки интересное описание товара в несколько строк. ',
          price: 10000
        },
        {
          img: 'http://sun9-27.userapi.com/sun9-81/s/v1/if1/zO5oA6Nt-lyk_mEjEBH6ZJFSg4-xMggN9oiad_4UG317hI8rrDYNu0fNPHbXsymcIlKr5ADD.jpg?size=200x219&quality=96&crop=20,0,420,460&ava=1',
          name: 'Наименование товара',
          desc: '',
          price: 10000
        }
      ]
    }
  }
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
}
</style>
