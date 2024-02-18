<template>
    <div class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
        <p class="text-xl py-2">
            <b>Tạo đề thi</b>
        </p>
        <!-- Chọn môn học -->
        <div class="p-4 flex justify-between">
            <Dropdown label="Môn học" :list="listSubject" iconClass="fa-solid fa-book-open" />
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
                <tr>
                    <td class="p-4">1</td>
                    <td class="p-4">
                        <Dropdown @change_value="addRow" type="thin" label="Chọn câu hỏi" :list="listQuestion"
                            iconClass="fa-solid fa-arrow-right" />
                    </td>
                    <td class="p-4">
                        <input type="number" min="0" max="10" id="asw3"
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

export default {
    name: 'MakeTestPage',
    layout: 'main',
    components: {
        Dropdown,
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
                    id: 1,
                    link: "#",
                    name: "1 + 1 = ?",
                    answ1: "2",
                    answ2: "3",
                    answ3: "4",
                    answ4: "5",
                    isTrue: "1"
                },
                {
                    id: 2,
                    link: "#",
                    name: "2 + 2 = ?",
                    answ1: "2",
                    answ2: "3",
                    answ3: "4",
                    answ4: "5",
                    isTrue: "3"
                }
            ],
            listTestQuestion: []
        }
    },
    methods: {
        addRow(id) {
            console.log("add new row")
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