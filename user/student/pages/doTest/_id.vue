<template>
    <div id="container" class="container p-4 shadow bg-yellow-50 rounded-lg m-auto">
        <div class="py-4 text-lg">
            Đề Thi <b>{{ exam.subject_name }}</b><br>
            Mã code: <b>{{ exam.code }}</b><br>
            Thời gian: <b>{{ exam.duration / 60 }} minutes</b>
        </div>

        <div>
            <form action="" method="post">
                <div class="header" id="myHeader">
                    <span id="timer"></span>
                    <progress :max="exam.duration" :value="exam.duration" class="progress progress--rest" id="progressBar">
                    </progress>

                </div>
                <div class="content">
                    <section>
                        <div v-for="(item, index) in exam.questions">
                            <p>{{ item.content }}</p>
                            <img v-if="item.image_path !== null" :src="'http://127.0.0.1:8000/' + item.image_path"
                                alt="Cheetah" />
                            <div v-for="(subItem, subIndex) in item.answers">
                                <input type="checkbox" :id="subItem.id" name="answer" :value="subItem.id">
                                <label :for="subItem.id">{{ subItem.content }}</label><br>
                            </div>
                            <hr class="dashed">
                        </div>
                        <input class="btn btn-default" type="submit" value="Submit the exam" name="start">
                    </section>
                </div>


            </form>
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

.content {
    max-width: 800px;
    margin: auto
}

.timer {
    max-width: 100px;
    margin: auto;
    height: 50px
}

hr.dashed {
    border-top: 3px dashed #bbb;
    margin-bottom: 20px
}

input[type=submit] {
    width: 100%;
    background-color: #04AA6D;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer
}

input:hover {
    background-color: #45a049;
}

.header {
    padding: 10px 16px;
    text-align: center;
}

.sticky {
    position: fixed;
    top: 0;
    width: 100%;
}

.sticky+.content {
    padding-top: 102px;
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
                url: `http://127.0.0.1:8000/student/exam/${this.$route.params.id}`,
                headers: {
                    'Content-Type': 'application/json',
                    'token': localStorage.getItem("token")
                },
            }).then(response => {
                console.log(response)
                this.exam = response.data;
                this.runTimer();
            });
        },
        runTimer() {
            const timerElement = document.getElementById("timer");
            const progressBar = document.getElementById("progressBar")
            var timerCounter = 10;
            console.log(progressBar);
            const interval = setInterval(() => {
                if (timerCounter <= 1) {
                    window.location.href = "../result";
                    clearInterval(interval);
                }
                timerCounter = timerCounter - 1;
                const minutes = Math.floor(timerCounter / 60);
                const seconds = timerCounter - minutes * 60;
                timerElement.innerText = minutes + ":" + seconds;
                progressBar.value = timerCounter;
            }, 1000);

            window.onscroll = function () { this.myFunction() };
        },
        myFunction() {
            var header = document.getElementById("myHeader");
            var sticky = header.offsetTop;
            if (window.pageYOffset > sticky) {
                header.classList.add("sticky");
            } else {
                header.classList.remove("sticky");
            }
        }
    },


}
</script>