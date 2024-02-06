<template>
  <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2">
      <b>Ngân hàng đề thi</b>
    </p>
    <!-- Chọn môn học -->
    <div class="p-4">
      <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-pencil" />
    </div>
    <!-- Danh sách ngân hàng đề -->
    <div class="p-4">
      <table class="w-full">
        <thead>
          <tr class="text-left">
            <th class="p-4">STT</th>
            <th class="p-4">Câu hỏi</th>
            <th class="p-4">Đáp án</th>
            <th class="p-4">Thay đổi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in listQuestion" :key="index">
            <td class="p-4">{{ index + 1 }}</td>
            <td class="p-4">{{ item.quest }}</td>
            <td class="p-4">{{ item.answ }}</td>
            <td class="p-4">
              <button class="px-2">
                <i class="fa-solid fa-pen"></i>
              </button>
              <button class="px-2">
                <i class="fa-solid fa-trash"></i>
              </button>
            </td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td class="p-4" colspan="4">
              <button class="bg-teddy-brow rounded-lg bold p-2 w-full">
                <i class="fa-solid fa-plus text-white"></i>
                <span class="text-white">Thêm mới câu hỏi</span>
              </button>
            </td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</template>

<script>
import Dropdown from '../../components/Dropdown.vue';

export default {
  name: 'MakeQuizPage',
  layout: 'main',
  components: {
    Dropdown
  },
  data() {
    return {
      listSubject: [
        {
          link: "#",
          name: "Toán học"
        },
        {
          link: "#",
          name: "Tiếng anh"
        }
      ],
      listQuestion: [
        {
          id: "1",
          quest: "1 + 1=",
          answ: "2"
        },
        {
          id: "1",
          quest: "2 + 3=",
          answ: "5"
        }
      ]
    }
  }

}
</script>

<style scoped>
* {
  color: #97704f;
}

.text-white {
  color: white !important;
}

thead {
  border-bottom: 1px solid #97704f;
}

.container {
  height: 90vh;
}
</style>
