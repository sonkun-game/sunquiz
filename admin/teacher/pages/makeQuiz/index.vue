<template>
  <div id="container" class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
    <p class="text-xl py-2">
      <b>Ngân hàng câu hỏi</b>
    </p>
    <!-- Chọn môn học -->
    <div class="p-4 flex gap-2">
      <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />
      <div>
        <label for="uploadFile"
          class="bg-teddy-brow cursor-pointer text-white font-medium rounded-lg text-sm px-5 py-2.5 text-center inline-flex items-center">
          <span class="px-4">Import file</span>
          <input @change="onFileChanged($event)" style="display: none;" id="uploadFile" name="uploadFile" type="file" />
        </label>
      </div>
    </div>
    <!-- Danh sách ngân hàng đề -->
    <div class="p-4">
      <table class="w-full">
        <thead>
          <tr class="">
            <th class="p-4 text-left">STT</th>
            <th class="p-4 text-left">Môn học</th>
            <th class="p-4 text-left">Hình ảnh</th>
            <th class="p-4 text-left">Câu hỏi</th>
            <th class="p-4">Thay đổi</th>
          </tr>
        </thead>
        <tbody>
          <tr class="hover:bg-orange-100 border-top-teddy-brow" v-for="(item, index) in listQuestion" :key="index">
            <td class="p-4">{{ index + 1 }}</td>
            <td class="p-4">{{ item.subject_name }}</td>
            <td>
              <img v-if="getImage(item.image_path) !== ''" class="question-image" :src="getImage(item.image_path)"
                alt="Question Image" />
            </td>
            <td class="p-4">{{ item.content }}</td>

            <td class="p-4" style="width: 100px;">
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
              <button @click="createQuiz()" class="bg-teddy-brow rounded-lg bold p-2 w-full">
                <i class="fa-solid fa-plus text-white"></i>
                <span class="text-white">Thêm mới câu hỏi</span>
              </button>

            </td>
          </tr>
          <tr v-else>
            <td class="p-4" colspan="2">
              <button @click="createQuiz()" class="bg-white text-teddy-brow rounded-lg bold p-2 w-full">
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
import axios from 'axios';

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
      pageSize: 1000,
      pageIndex: 0,
      isCreated: false,
      isDeleted: false,
      listSubject: [],
      listQuestion: [],
      quiz: {
        subjectId: 0,
        content: "",
        image_path: "",
        
      }
    }
  },
  mounted() {
    this.fetchData();
    this.fetchSubject();
  },
  methods: {
    getImage(image) {
      if (image == null || image == "") return "";
      try {
        var imgPath = require(`~/public/${image}`);
        return imgPath;
      } catch (e) { }
      return "";
    },
    createQuiz() {
      this.isCreated = !this.isCreated;
    },
    deleteQuiz() {
      this.isDeleted = !this.isDeleted;
    },
    fetchData() {
      axios({
        method: 'get',
        url: `http://127.0.0.1:8000/admin/question?page_size=${this.pageSize}&page_index=${this.pageIndex}`,
        headers: {
          'Content-Type': 'application/json',
          'token': localStorage.getItem("token")
        },
      }).then(response => {
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
              this.listQuestion.push(element);
            }
          });
        } else {
          this.listQuestion = list;
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
    },
    toBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve(reader.result);
        reader.onerror = reject;
      })
    },
    async onFileChanged(event) {
      const target = event.target;
      var file = null;
      if (target && target.files) {
        console.log(target.files[0]);
        file = target.files[0];
      }
      console.log(file);

      var formData = new FormData();
      formData.append("file", target.files[0]);
      console.log(formData);

      if (file != null) {
          try {
            axios({
              method: 'post',
              url: 'http://127.0.0.1:8000/import/',
              responseType: 'json',
              headers: {
                'Content-Type': 'multipart/form-data',
                'Token': localStorage.getItem("token")
              },
              data: formData
            }).then(response => {
              alert("Import thành công");
              location.reload();
            });
          } catch (e) {
            alert("ERROR !");
            console.log(e);
          }
        } else {
          alert("fileUpload is null !");
        }
    }
  }
}
</script>

<style scoped>
div {
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

.container {}

.question-image {
  max-width: 150px;
}
</style>
