<template>
  <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2">
      <b>Quản lý đề thi</b>
    </p>
    <!-- Chọn môn học -->
    <div class="p-4 flex justify-between">
      <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />

      <a href="/makeTest/create">
        <button class="bg-teddy-brow text-white font-medium rounded-lg text-sm px-5 py-2.5">Tạo đề thi</button>
      </a>

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
            <th class="p-4 text-left">Mô tả</th>
            <th class="p-4 text-left">Thời gian thi (phút)</th>
            <th class="p-4 text-left">Ngày bắt đầu</th>
            <th class="p-4 text-left">Ngày kết thúc</th>
            <th class="p-4">Thay đổi</th>
          </tr>
        </thead>
        <tbody>
          <tr class="hover:bg-orange-100" v-for="(item, index) in listTest" :key="index">
            <td class="p-4">{{ index + 1 }}</td>
            <td class="p-4">{{ item.subject_name }}</td>
            <td class="p-4">{{ item.code }}</td>
            <td class="p-4">{{ item.num_of_question }}</td>
            <td class="p-4">{{ item.description }}</td>
            <td class="p-4">{{ item.duration }}</td>
            <td class="p-4">{{ item.time_start }}</td>
            <td class="p-4">{{ item.time_end }}</td>
            <td class="p-4">
              <button class="px-2">
                <i class="fa-solid fa-pen"></i>
              </button>
              <button @click="deleteQuiz()" class="px-2">
                <i class="fa-solid fa-trash"></i>
              </button>
            </td>
          </tr>
        </tbody>
        <tfoot>
        </tfoot>
      </table>
    </div>

    <!-- Confirm Delete Box -->
    <ConfirmBox @cancle_delete="deleteQuiz" text="Bạn có chắc muốn xóa câu hỏi này ? " :show="isDeleted"></ConfirmBox>
  </div>
</template>

<script>
import Dropdown from '../../components/Dropdown.vue';
import ConfirmBox from '../../components/ConfirmBox.vue';
import axios from 'axios';

export default {
  name: 'MakeTestPage',
  layout: 'main',
  components: {
    Dropdown,
    ConfirmBox
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
      listTest: [],
      isDeleted: false,
    }
  },
  mounted() {
    this.fetchData();
    this.fetchSubject();
  },
  methods: {
    deleteQuiz() {
      this.isDeleted = !this.isDeleted;
    },
    fetchData() {
      axios({
        method: 'get',
        url: 'http://127.0.0.1:8000/admin/exam',
        headers: {
          'Content-Type': 'application/json',
          'token': localStorage.getItem("token")
        },
      }).then(response => {
        console.log(response.data);
        var list = response.data;
        var subject = this.$route.query.subject;
        var key = "";
        switch (subject) {
          case "VAN":
            key = "Môn văn"
            break;
          case "TOAN":
            key = "Môn Toán"
            break;
          case "TIENG_ANH":
            key = "Môn tiếng anh"
            break;
          case "TIN_HOC":
            key = "Môn văn"
            break;
          default:
            break;
        }
        if (key !== "") {
          list.forEach(element => {
            if (key.toUpperCase() === element.subject_name.toUpperCase()) {
              this.listTest.push(element);
            }
          });
        } else {
          this.listTest = list;
        }
      });
    },
    fetchSubject() {
      axios({
        method: 'get',
        url: `http://127.0.0.1:8000/admin/subject`,
        headers: {
          'Content-Type': 'application/json',
          'token': localStorage.getItem("token")
        },
      }).then(response => {
        this.listSubject = response.data;
      });
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