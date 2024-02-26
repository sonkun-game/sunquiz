<template>
    <div>
        <form class="bg-yellow-50" action="" method="post">
            <h1>Your score: {{ score }} </h1>
            <h3>Submit at: {{ time }} </h3>
            <input class="button" type="submit" value="CONFIRM" name="start" onclick="window.location='/login';">
        </form>
    </div>
</template>

<script>
export default {
    name: "ResultPage",
    layout: "main",
    data() {
        return {
            score: 0,
            time: 0
        }
    }
}
</script>

<style scoped>
/* Add some style to the form */
form {
    border: 2px solid #ccc;
    width: 300px;
    margin: 0 auto;
    padding: 20px;
}

/* Style the input fields */
input[type=text],
input[type=password] {
    width: 100%;
    margin: 10px 0;
    padding: 10px;
    border: 1px solid #ccc;
}

/* Style the submit button */
input[type=submit] {
    width: 100%;
    background-color: #04AA6D;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
}

/* Style the submit button on hover */
input[type=submit]:hover {
    background-color: #45a049;
}
</style>