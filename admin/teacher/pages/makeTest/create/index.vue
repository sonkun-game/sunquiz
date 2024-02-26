<template>
    <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
        <p class="text-xl py-2">
            <b>Tạo đề thi</b>
        </p>
        <!-- Chọn môn học -->
        <div class="p-4 flex justify-between">
            <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />
        </div>
        <p class="text-lg font-bold p-4">Id môn học : {{ subjectId }}</p>
        <!-- Nhập code -->
        <div class="p-2">
            <label for="code">Code: </label>
            <input id="code" name="code" class="p-2 bg-transparent border-bottom-teddy-brow" v-model="code" />
        </div>
        <div class="p-2">
            <label for="time_start">Bắt đầu: </label>
            <input type="date" id="time_start" name="time_start" class="p-2 bg-transparent border-teddy-brow rounded-lg" />
        </div>
        <div class="p-2">
            <label for="time_end">Kết thúc: </label>
            <input type="date" id="time_end" name="time_end" class="p-2 bg-transparent border-teddy-brow rounded-lg" />
        </div>
        <div class="p-2">
            <label for="duration">Thời gian: </label>
            <input type="number" min="0" id="duration" name="duration" class="p-2 bg-transparent border-teddy-brow rounded-lg" />
        </div>
        <div class="p-2">
            <label for="duration">số câu hỏi: </label>
            <input type="number" value="2" readonly id="numOfQuest" name="numOfQuest" class="p-2 bg-transparent border-teddy-brow rounded-lg" />
        </div>
        <div class="p-2">
            <label for="description">Mô tả: </label><br>
            <textarea id="description" name="description" class="p-2 bg-transparent rounded-lg"></textarea>
        </div>

        <table>
            <thead>
                <tr>
                    <th class="p-4 text-left">STT</th>
                    <th class="p-4 text-left">Câu hỏi</th>
                    <th class="p-4 text-left">Điểm số</th>
                </tr>
            </thead>
            <tbody>
                <tr>

                </tr>
                <tr v-for="item in 2" :key="item">
                    <td class="p-4">{{ item }}</td>
                    <td class="p-4">
                        <Dropdown @change_value="addRow" type="thin" label="Chọn câu hỏi" :list="listQuestion" :dropType="2"
                            iconClass="fa-solid fa-arrow-right" />
                    </td>
                    <td class="p-4">
                        <input type="number" value="5" id="asw3" readonly
                            class="p-2 bg-transparent border-bottom-teddy-brow" />
                    </td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td class="p-4" colspan="3">
                        <button class="bg-teddy-brow rounded-lg bold p-2 w-full">
                            <i class="fa-solid fa-hammer text-white"></i>
                            <span class="text-white">Tạo đề thi</span>
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
    },
    data() {
        return {
            listSubject: [],
            listQuestion: [],
            subjectId: "1",
            code: "",
            pageSize: 1000,
            pageIndex: 0,
        }
    },
    methods: {
        addRow(id) {
            console.log("add new row")
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
                    console.log(item.code);
                    if (item.code === subject) {
                        this.subjectId = item.id;
                    }
                });
            });
        },
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