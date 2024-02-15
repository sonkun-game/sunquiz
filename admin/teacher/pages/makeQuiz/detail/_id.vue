<template>
  <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2 cursor-pointer">
      <NuxtLink to="../">
        <i class="fa-solid fa-left-long"></i>
      </NuxtLink>
      <span class="px-2"><b>Thông tin chi tiết câu hỏi {{ id }}</b></span>
    </p>


    <div class="p-4 border-teddy-brow">
      <div class="text-xl p-2">
        <b>1 + 1 = ?</b>
      </div>
      <div>
        <div class="p-2">
          <img class="question-image" src="../../../static/img/math.jpg" />
        </div>
        <div class="p-2">
          <ul class="cursor-pointer">
            <li class="flex">
              <div class="answ border-teddy-brow p-2"> 
                A: 2 <span class="py-2 text-lime-400"><i class="fa-solid fa-check font-bold"></i></span>
              </div>
              <div class="answ border-teddy-brow p-2"> B: 3 </div>
            </li>
            <li class="flex">
              <div class="answ border-teddy-brow p-2"> C: 4 </div>
              <div class="answ border-teddy-brow p-2"> D: 5 </div>
            </li>
          </ul>
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped>
p, div {
  color: #97704f;
}

.container {
  height: 90vh;
}

.question-image {
  max-width: 400px;
}

.answ {
  width: 400px;
}
</style>

<script>
export default {
  name: 'MakeQuizPage',
  layout: 'main',
  computed: {
    id() {
      return this.$route.params.id;
    }
  }
}
</script>

