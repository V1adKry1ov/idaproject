<template>
    <div class="create-form">
        <div class="input-div">
            <p class="form-input-text">Наименование товара</p>
            <input type="text" class="form-input" placeholder="Введите наименование товара">
        </div>
        <div class="input-div">
            <p class="form-input-text">Описание товара</p>
            <textarea class="form-textarea" placeholder="Введите описание товара"></textarea>
        </div>
        <div class="input-div">
            <p class="form-input-text">Ссылка на изображение товара</p>
            <input type="text" class="form-input" placeholder="Введите ссылку">
        </div>
        <div class="input-div">
            <p class="form-input-text">Цена товара</p>
            <input type="text" class="form-input" placeholder="Введите цену">
        </div>
        <button class="add-button">Добавить товар</button>
    </div>
</template>
<script>

export default {
  name: 'CreateForm',
}
</script>

<style lang="scss" scoped>
@use "src/consts/colors" as colors;
.create-form {
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
}
.form-input-text::after {
    content: "";
    background: red;
    height: 4px;
    width: 4px;
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
    
    
}

.add-button {
    background: colors.$grey-bg;
    border-radius: 10px;
    font-weight: 600;
    font-size: .75rem;
    line-height: .9375rem;
    padding: .625rem 0;
    border: none;
    color: colors.$grey-primary;
}
</style>