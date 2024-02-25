<template>
    <div id="container" class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
        <div class="py-4 text-lg">
            Đề Thi <b>{{ exam.subject_name }}</b><br>
            Mã code: <b>{{ exam.code }}</b><br>
            Thời gian: <b>{{ exam.duration / 60 }} minutes</b>
        </div>

    </div>
</template>

<style scoped>
body {
    font-family: Arial, Helvetica, sans-serif;
}

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

<script>
import axios from 'axios'

export default {
    name: "studentExamList",
    layout: "main",
    data() {
        return {
            exam: {}
        }
    },
    mounted() {
        this.fetchData();
    },
    computed: {
        id() {
            return this.$route.params.id;
        }
    },
    methods: {
        fetchData() {
            axios({
                method: 'get',
                url: `http://127.0.0.1:8080/student/exam/${this.$route.params.id}`,
                headers: {
                    'Content-Type': 'application/json',
                    'token': localStorage.getItem("token")
                },
            }).then(response => {
                console.log(response)
                this.exam = response.data;
            });
        },
    },


}
</script>