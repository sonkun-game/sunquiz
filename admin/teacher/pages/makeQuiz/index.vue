<template>
  <div id="container" class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2">
      <b>Ngân hàng câu hỏi</b>
    </p>
    <!-- Chọn môn học -->
    <div class="p-4">
      <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />
    </div>
    <!-- Danh sách ngân hàng đề -->
    <div class="p-4">
      <table class="w-full">
        <thead>
          <tr class="">
            <th class="p-4 text-left">STT</th>
            <th class="p-4 text-left">Câu hỏi</th>
            <th class="p-4 text-left">Hình ảnh</th>
            <th class="p-4 text-left">Đáp án</th>
            <th class="p-4">Thay đổi</th>
          </tr>
        </thead>
        <tbody>
          <tr class="hover:bg-orange-100 border-top-teddy-brow" v-for="(item, index) in listQuestion" :key="index">
            <td class="p-4">{{ index + 1 }}</td>
            <td class="p-4">{{ item.quest }}</td>
            <td class="">
              <img class="question-image" src="../../static/img/math.jpg" />
            </td>
            <td class="p-4">
              {{ item.answ }}
            </td>
            <td class="p-4">
              <NuxtLink :to="'/makeQuiz/detail/' + item.id">
                <i class="fa-solid fa-eye"></i>
              </NuxtLink>
              <NuxtLink :to="'/makeQuiz/edit/' + item.id">
                <i class="fa-solid fa-pen"></i>
              </NuxtLink>
              <button @click="deleteQuiz()" class="px-2">
                <i class="fa-solid fa-trash"></i>
              </button>
            </td>
          </tr>
        </tbody>
        <tfoot class="border-top-teddy-brow">
          <tr v-if="isCreated">
            <td class="p-4"><b>Tạo câu hỏi mới</b></td>
            <td class="p-4">
              <input id="quest" class="p-2 bg-transparent border-teddy-brow" placeholder="Nhập câu hỏi" />
            </td>
            <td class="p-4">
              <input id="image" type="file" class="p-2" placeholder="Upload file" />
            </td>
            <td class="p-4">
              <div>
                <label for="asw1">A: </label>
                <input id="asw1" class="p-2 bg-transparent border-bottom-teddy-brow" />
              </div>
              <div>
                <label for="asw2">B: </label>
                <input id="asw2" class="p-2 bg-transparent border-bottom-teddy-brow" />
              </div>
              <div>
                <label for="asw3">C: </label>
                <input id="asw3" class="p-2 bg-transparent border-bottom-teddy-brow" />
              </div>
              <div>
                <label for="asw4">D: </label>
                <input id="asw4" class="p-2 bg-transparent border-bottom-teddy-brow" />
              </div>
            </td>
          </tr>
          <tr v-if="!isCreated">
            <td class="p-4" colspan="5">
              <button  @click="createQuiz()" class="bg-teddy-brow rounded-lg bold p-2 w-full">
                <i class="fa-solid fa-plus text-white"></i>
                <span class="text-white">Thêm mới câu hỏi</span>
              </button>

            </td>
          </tr>
          <tr v-else>
            <td class="p-4" colspan="2">
              <button  @click="createQuiz()" class="bg-white text-teddy-brow rounded-lg bold p-2 w-full">
                <i class="fa-solid fa-x"></i>
                <span>Hủy</span>
              </button>
            </td>
            <td class="p-4" colspan="3">
              <button class="bg-teddy-brow rounded-lg bold p-2 w-full">
                <i class="fa-solid fa-hammer text-white"></i>
                <span class="text-white">Tạo</span>
              </button>
            </td>
          </tr>
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

export default {
  name: 'MakeQuizPage',
  layout: 'main',
  components: {
    Dropdown,
    ConfirmBox
},
  computed: {},
  data() {
    return {
      isCreated: false,
      isDeleted: false,
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
          id: 1,
          quest: "1 + 1=",
          answ: "2"
        },
        {
          id: 2,
          quest: "2 + 3=",
          answ: "5"
        },
        {
          id: 3,
          quest: "2 + 3=",
          answ: "5"
        }
      ]
    }
  },
  methods: {
    createQuiz() {
      this.isCreated = !this.isCreated;
    },
    deleteQuiz() {
      this.isDeleted = !this.isDeleted;
    }
  }
}
</script>

<style scoped>
* {
  color: #97704f;
}
.bg-transparent {
  background-color: transparent;
  outline: none;
  color: #78583d;
}
::placeholder {
  color: #78583d;
}
.text-white {
  color: white !important;
}

.list-question {
  display: block;
  height: 200px;
  overflow-y: auto;
}
.container {
 
}
.question-image {
  max-width: 150px;
}
</style>
