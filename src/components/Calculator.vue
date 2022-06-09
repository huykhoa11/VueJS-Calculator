<template>
    <div class="box">
        <div class="header">
            <div class="C-btn" @click="reset()">
                C
            </div>

            <div class="screen">
                {{ result }}
            </div>
        </div>

    <div class="main">
            <div class="btn" v-for="(value, key) in buttons" :key="key" 
                @click="btnClick(value)">
                {{ value }}
            </div>
        </div>
    </div>
</template>

<script>

export default {

    components: {
    },

    data() {
        return {
            result: "0",
            init: true,
            newCal: true,
            operator: "",
            previous: "",
            buttons: ["7", "8", "9", "+", "4", "5", "6", "-", "1", "2", "3", "÷", "0", ".", "=", "x"],
        }
    },

    methods: {
        btnClick(v) {
            if(this.init == true) this.result = ""; this.init = false;

            if(["+", "-", "÷", "x"].includes(v)){
                if(v == "÷") this.operator = "/";
                else if(v == "x") this.operator = "*";
                else this.operator = v;

                this.previous = this.result;
                this.newCal = false;

            }
            else if(["+", "-", "÷", "x"].includes(v) == false && v != "="){
                if(this.newCal == false) this.result = "";
                this.result += v;
                this.newCal = true;
            }

            if(v == "=") {
                this.result = eval(this.previous + this.operator + this.result);
                this.previous = "";
                this.operator = "";
            }
        },

        reset() {
            this.init = true;
            this.result = "0";
        }
    }, 

}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kdam+Thmor+Pro&family=Nunito:wght@600&display=swap');

.box {
    font-family: 'Kdam Thmor Pro', sans-serif;
    font-family: 'Nunito', sans-serif;
    width: 300px;
    height: 350px;
    background-color: black;
    position: absolute;
}

.header {
    width: 280px;
    height: 50px;
    margin: 10px;
}

.C-btn {
    float: left;
    color: white;
    background-color: crimson;
    width: 50px;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: X-large;
    box-shadow: 2px 2px #555;
}

.C-btn:hover {
    cursor: pointer;
}

.C-btn:active {
    box-shadow: 2px 2px black;
}

.screen {
    float: right;
    width: 75%;
    height: 100%;
    padding-right: 8px;
    background-color: darkgreen;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    color: white;
    font-size: xx-large;
}

.main {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
}

.btn {
    color: black;
    box-shadow: 2px 2px #bbb;
    height: 50px;
    width: 60px;
    padding: 3px;
    margin: 5px 0;
    background-color: antiquewhite;
    font-size: x-large;
    /* text-align: center; */
    display: flex;
    justify-content: center;
    align-items: center;
}

.btn:hover {
    cursor: pointer;
}

.btn:active {
    box-shadow: 2px 2px black;
}

</style>