<template>
  <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2">
      <b>Quản lý đề thi</b>
    </p>
    <!-- Chọn môn học -->
    <div class="p-4 flex justify-between">
      <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />

      <button class="bg-teddy-brow text-white font-medium rounded-lg text-sm px-5 py-2.5">Tạo đề thi</button>
    </div>
    <!-- Danh sách ngân hàng đề -->
    <div class="p-4">
      <table class="w-full">
        <thead>
          <tr class="">
            <th class="p-4 text-left">STT</th>
            <th class="p-4 text-left">Đề thi</th>
            <th class="p-4 text-left">Mã đề</th>
            <th class="p-4 text-left">Số câu hỏi</th>
            <th class="p-4 text-left">Thời gian thi (phút)</th>
            <th class="p-4 text-left">Thời hạn hiệu lực</th>
            <th class="p-4">Thay đổi</th>
          </tr>
        </thead>
        <tbody>
          <tr class="hover:bg-orange-100" v-for="(item, index) in listTest" :key="index">
            <td class="p-4">{{ index + 1 }}</td>
            <td class="p-4">{{ item.name }}</td>
            <td class="p-4">{{ item.code }}</td>
            <td class="p-4">{{ item.questNum }}</td>
            <td class="p-4">{{ item.time }}</td>
            <td class="p-4">{{ item.expired }}</td>
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
        </tfoot>
      </table>
    </div>
  </div>
</template>

<script>
import Dropdown from '../../components/Dropdown.vue';

export default {
  name: 'MakeTestPage',
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
      listTest: [
        {
          id: 1,
          name: "Đề kiểm tra môn Toán học kỳ 1",
          code: "MAE1-20240207",
          questNum: "18",
          time: "45",
          expired: "2024-02-07T14:00:00",
        },
        {
          id: 2,
          name: "Đề kiểm tra môn Toán học kỳ 2",
          code: "MAE1-20240228",
          questNum: "18",
          time: "45",
          expired: "2024-02-28T14:00:00",
        },
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