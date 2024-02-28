<template>
    <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
        <p class="text-xl py-2">
            <b>Tạo đề thi</b>
        </p>
        <!-- Chọn môn học -->
        <div class="p-4 flex gap-2">
            <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />
            <Dropdown @change_value="setExam" label="Đề thi" :list="listExam" :dropType="3"
                iconClass="fa-solid fa-list-check" />
        </div>
        <p class="text-lg font-bold p-4">Tên môn học : {{ subjectName }}</p>

        <table>
            <thead>
                <tr>
                    <th class="p-4 text-left">STT</th>
                    <th class="p-4 text-left">Câu hỏi</th>
                    <th class="p-4 text-left">Điểm số</th>
                    <th class="p-4 text-left">Mix Choice</th>
                </tr>
            </thead>
            <tbody>
                <tr>

                </tr>
                <tr v-for="item in 1" :key="item">
                    <td class="p-4">{{ item }}</td>
                    <td class="p-4">
                        <Dropdown @change_value="setQuestion" type="thin" label="Chọn câu hỏi" :list="listQuestion"
                            :dropType="4" iconClass="fa-solid fa-arrow-right" />
                    </td>
                    <td class="p-4">
                        <input type="number" value="1" id="asw" class="p-2 bg-transparent border-bottom-teddy-brow" />
                    </td>
                    <td class="p-4">
                        <input type="checkbox" id="asw" class="p-2 bg-transparent border-bottom-teddy-brow" />
                    </td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td class="p-4" colspan="3">
                        <button @click="submitQuest()" type="button" class="bg-teddy-brow rounded-lg bold p-2 w-full">
                            <i class="fa-solid fa-hammer text-white"></i>
                            <span class="text-white">Insert câu hỏi vào đề thi</span>
                        </button>
                    </td>
                </tr>
            </tfoot>
        </table>
    </div>
</template>
  
<script>
import Dropdown from '../../../components/Dropdown.vue';
import axios from 'axios';

export default {
    name: 'MakeTestPage',
    layout: 'main',
    components: {
        Dropdown,
    },
    mounted() {
        this.fetchSubject();
        this.fetchData();
        this.fetchExam();
    },
    data() {
        return {
            listSubject: [],
            listQuestion: [],
            listExam: [],
            listQuestion: [],
            examId: "",
            questionId: "",
            subjectName: "1",
            code: "",
            pageSize: 1000,
            pageIndex: 0,
        }
    },
    methods: {
        setQuestion(id) {
            this.questionId = id;
        },
        setExam(id) {
            this.examId = id;
        },
        submitQuest() {
            if (this.examId && this.questionId) {
                axios({
                    method: 'post',
                    url: `http://127.0.0.1:8000/admin/exam/${this.examId}?question_id=${this.questionId}&mark=1&mix_choice=1`,
                    responseType: 'json',
                    headers: {
                        'Content-Type': 'application/json',
                        'token': localStorage.getItem("token")
                    },
                }).then(response => {
                    var respData = response.data;
                    alert("Đã thêm câu hỏi thành công !");
                    location.reload();
                });
            } else {
                alert("Hãy nhập thông tin đầy đủ")
            }
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
                console.log(this.listQuestion);
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
                var subject = this.$route.query.subject;
                this.listSubject.forEach(item => {
                    if (item.code === subject) {
                        this.subjectName = item.name;
                    }
                });
            });
        },
        fetchExam() {
            axios({
                method: 'get',
                url: `http://127.0.0.1:8000/admin/exam`,
                headers: {
                    'Content-Type': 'application/json',
                    'token': localStorage.getItem("token")
                },
            }).then(response => {
                console.log("ddd", response.data);
                this.listExam = response.data;
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
    height: 150vh;
}
</style>