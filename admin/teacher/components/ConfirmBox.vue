<template>
    <div v-if="show" class="cfbox-container p-4 bg-yellow-50 border-teddy-brow">
        <div class="p-4 text-lg text-center">
            <b>{{ text }}</b>
        </div>
        <div class="p-4 w-full flex gap-2">
            <button @click="cancleConfirm" class="p-2 bg-white text-teddy-brow rounded-lg">Thôi không xóa</button>
            <button class="p-2 bg-teddy-brow rounded-lg">Xóa !!</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "ConfirmBox",
    props: {
        id: "",
        text: "",
        show: false,
    },
    methods: {
        cancleConfirm() {
            this.$emit('cancle_delete')
        }
    }
}
</script>

<style scoped>
.cfbox-container {
    width: 400px;
    height: 150px;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
}
</style>