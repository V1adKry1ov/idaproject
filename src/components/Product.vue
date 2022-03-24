<template>
    <div class="product" @mouseover="isDeleteButtonShow = true" @mouseleave="isDeleteButtonShow = false">
        <div v-if="isDeleteButtonShow" @click="deleteProduct" class="deleteButton">
            <img src="../assets/delete.svg" alt="delet button">
        </div>
        <img alt="img product" class="product__img" :src="srcImg">
        <div class="product__body">
            <div class="product__text-div">
                <p class="product__name">{{product.name}}</p>
                <p class="product__description">{{product.desc}}</p>
            </div>
            <h3 class="product__price">{{product.price.toLocaleString('ru-RU')}} руб.</h3>
        </div>
    </div>
</template>
<script>
export default {
    name: 'App',
    props: {
        product: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            isDeleteButtonShow: false,
            srcImg: this.product.img
        }
    },
    methods: {
        deleteProduct() {
            this.$emit('delete-product')
        }
    },
    mounted() {
        let img = new Image;
        img.src = this.product.img;
        let vm = this;

        img.onload = function () {
            vm.srcImg = vm.product.img
        };

        img.onerror = function () {
            vm.srcImg = 'data:image/jpeg;base64,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';
        };
    }
}
</script>
<style lang="scss" scoped>
@use "src/consts/colors" as colors;
.product {
    display: flex;
    flex-direction: column;
    position: relative;
    height: 26.4375rem;
    width: 20.75rem;
    background: colors.$white-primary;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;

    &__img {
        width: 20.75rem;
        height: 12.5rem;
        border-radius: 4px;

    }

    &__body {
        flex: 1;
        position: relative;
        padding: 1rem 1rem 1.5rem 1rem;
    }

    &__text-div {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }
    
    &__name {
        max-height: 1.5625rem;
        overflow: hidden;
        font-weight: 600;
        font-size: 1.25rem;
        line-height: 1.5625rem;
        color: colors.$black-primary;
    }

    &__description {
        max-height: 5rem;
        overflow: hidden;
        font-weight: 400;
        font-size: 1rem;
        line-height: 1.25rem;
        color: colors.$black-primary;
    }

    &__price {
        font-weight: 600;
        font-size: 1.5rem;
        line-height: 1.875rem;
        color: colors.$black-primary;
        position: absolute;
        bottom: 1.5rem;
    }
}
.deleteButton {
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    top: -.5rem;
    right: -.5rem;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    width: 2rem;
    height: 2rem;
    background: colors.$red-primary;
}
</style>
