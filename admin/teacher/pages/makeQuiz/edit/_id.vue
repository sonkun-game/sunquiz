<template>
  <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2 cursor-pointer">
      <NuxtLink to="../">
        <i class="fa-solid fa-left-long"></i>
      </NuxtLink>
      <span class="px-2"><b>Chỉnh sửa câu hỏi {{ id }} :</b></span>
    </p>


    <div class="p-4 border-teddy-brow">
      <div class="text-xl p-2">
        <div>
          <label for="quest">Câu hỏi : </label>
          <input id="quest" class="p-2 bg-transparent border-bottom-teddy-brow" />
        </div>
      </div>
      <div>
        <div class="p-2">
          <label for="upload_image"><b> Upload ảnh </b></label><br>
          <input id="upload_image" type="file" />
        </div>
        <div class="p-2">
          <ul class="cursor-pointer">
            <li>
              <div>
                <label for="asw1">A: </label>
                <input id="asw1" class="p-2 bg-transparent border-bottom-teddy-brow" />
                <input class="px-2" id="is_true_1" type="checkbox" />
              </div>
            </li>
            <li>
              <div>
                <label for="asw2">B: </label>
                <input id="asw2" class="p-2 bg-transparent border-bottom-teddy-brow" />
                <input class="px-2" id="is_true_2" type="checkbox" />
              </div>
            </li>
            <li>
              <div>
                <label for="asw3">C: </label>
                <input id="asw3" class="p-2 bg-transparent border-bottom-teddy-brow" />
                <input class="px-2" id="is_true_3" type="checkbox" />
              </div>
            </li>
            <li>
              <div>
                <label for="asw4">D: </label>
                <input id="asw4" class="p-2 bg-transparent border-bottom-teddy-brow" />
                <input class="px-2" id="is_true_4" type="checkbox" />
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="flex gap-4 p-4" style="width: 400px;">
        <button class="bg-white text-teddy-brow rounded-lg bold p-2 w-full">
          <i class="fa-solid fa-x"></i>
          <span>Hủy</span>
        </button>
        <button class="bg-teddy-brow rounded-lg bold p-2 w-full">
          <i class="fa-solid fa-hammer text-white"></i>
          <span class="text-white">Sửa</span>
        </button>
      </div>
    </div>

  </div>
</template>

<style scoped>
p,
div {
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
  name: 'MakeQuizEditPage',
  layout: 'main',
  computed: {
    id() {
      return this.$route.params.id;
    }
  }
}
</script>

