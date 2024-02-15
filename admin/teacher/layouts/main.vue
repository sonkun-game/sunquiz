
<template>
    <div class="layout-container no-scrollbar">
        <nav class="navbar w-100 h-15 px-4 py-1 flex justify-between items-center shadow">
            <div class="flex items-center gap-2 cursor-pointer">
                <img class="logo" src="../static/img/logo.png" alt="logoSunQuiz" />
                <span class="text-base pr-4 text-white">SunQuiz</span>
                <a href="/makeQuiz" class="text-base px-2 bg-teddy-brow">Ngân hàng câu hỏi</a>
                <a href="/makeTest" class="text-base px-2 bg-teddy-brow">Quản lý đề thi</a>
            </div>

            <div class="grow"></div>
            <div class="p-2 flex items-center gap-3 text-white cursor-pointer">
                <i class="text-lg fa-solid fa-circle-user"></i>
                <span>Hoang Thai Son</span>
            </div>
        </nav>
        <div class="flex">
            <!-- Main Bar -->
            <div class="custom-bar w-screen grow">
                <div>
                    <client-only>
                        <template #placeholder>
                            <div class="w-screen h-screen fixed flex overflow-hidden">
                                <div class="text-blue-500 text-4xl my-auto" style="margin-left: 30%">
                                    <img class="w-64 h-64" src="~/static/img/loading.png" alt="loading..." />
                                </div>
                            </div>
                        </template>
                        <div class="content w-full px-8 py-4 nuxt_container no-scrollbar overflow-scroll">
                            <Nuxt />
                        </div>
                    </client-only>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'mainV2Layout',
    data() {
        return {
            authenURL: "",
        }
    },
    computed: {
    },
}

</script>
  
<style scoped>
div,
a,
li,
span {
    font-family: Inter, sans-serif;
    font-size: 14px;
}

.navbar {
    background-color: #97704f;
}

.logo{
    max-width: 50px;
}

div.title {
    font-weight: 600;
}

.bg-gland {
    background-color: #030712;
}

.drop_down_style {
    position: absolute;
    right: 25px;
    top: 65px;
}

.nuxt_container {
    height: 93vh;
}

.no-scrollbar::-webkit-scrollbar {
    display: none;
}

.no-scrollbar {
    -ms-overflow-style: none;
    scrollbar-width: none;
}

.content {
    background-color: cornsilk;
    background-image: url('../static/img/bg.jpg');
    background-repeat: repeat;
    background-size: 10%;
}

.layout-container {
    overflow: scroll;
    height: 100vh;
}
</style>