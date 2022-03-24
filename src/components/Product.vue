<template>
    <div class="product">
        <img :src="product.img" alt="img product" class="product__img">
        <div class="product__body">
            <div class="product__text-div">
                <p class="product__name">{{product.name}}</p>
                <p class="product__description">{{product.desc}}</p>
            </div>
            <h3 class="product__price">{{product.price}} руб.</h3>
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
        return {}
    }
}
</script>
<style lang="scss" scoped>
@use "src/consts/colors" as colors;
.product {
    display: flex;
    flex-direction: column;
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
</style>
