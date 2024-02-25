<template>
    <div id="container" class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
        <div class="content">
            <h2 class="text-lg py-4">Available Exam</h2>
            <div class="row">
                <div class="column" v-for="(item, index) in listExam" :key="index">
                    <div class="card">
                        <h3 value="">{{ item.code }}</h3>
                        <p></p>
                        <p>Duration: {{ item.duration / 60 }} minutes</p>
                        <p>Subject: {{ item.subject }}</p>
                        <a :href="'/doTest/' + item.id">
                            <button class="btn btn-default">
                                Vào thi
                            </button>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
* {
    box-sizing: border-box;
}

body {
    font-family: Arial, Helvetica, sans-serif;
}

/* Float four columns side by side */
.column {
    float: left;
    width: 25%;
    padding: 0 10px;
}

/* Remove extra left and right margins, due to padding */
.row {
    margin: 0 -5px;
}

/* Clear floats after the columns */
.row:after {
    content: "";
    display: table;
    clear: both;
}

/* Responsive columns */
@media screen and (max-width: 600px) {
    .column {
        width: 100%;
        display: block;
        margin-bottom: 20px;
    }
}

.content {
    max-width: 100%;
    margin: auto;
}

.instruction {
    max-width: 100%;
    margin: auto;
}


/* Style the counter cards */
.card {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    padding: 16px;
    text-align: center;
}

input[type=submit],
button {
    width: 100%;
    background-color: #97704f;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
    border-radius: 15px;
    padding: 5px;
    margin-top: 9px;
}

input[type=submit]:hover,
button:hover {
    background-color: white;
    color: #78583d;
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
            listExam: []
        }
    },
    mounted() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            axios({
                method: 'get',
                url: `http://127.0.0.1:8080/student/exam`,
                headers: {
                    'Content-Type': 'application/json',
                    'token': localStorage.getItem("token")
                },
            }).then(response => {
                console.log(response)
                this.listExam = response.data;
            });
        },
    },


}
</script>