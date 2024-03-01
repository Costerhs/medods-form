<template>
    <div class="modal">
        <div class="modal__info">
            <h1>Новый клиент успешо создан!</h1>
            <button @click="$emit('restart')">Продолжить</button>
        </div>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
.modal {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .modal__info {
        background: white;
        padding: 40px;
        border-radius: 20px;
        button {
            width: 200px;
            height: 50px;
            border-radius: 10px;
            border: 0;
            background: rgb(1, 206, 1);
            color: white;
            cursor: pointer;
        }
    }
}
</style>