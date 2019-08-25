<template>
    <div>
         <div id="screen" :class="state" @click="onClickScreen">{{message}}</div>
         <div>
             <div>average: {{average}}</div>
             <button @click="onReset">reset</button>
         </div>
    </div>
</template>

<script>
let startTime = 0;
let endTime = 0;
let timeout = null;
export default {
    data() {
        return {
            result: [],
            state: "waiting",
            message: 'start with click!',
        }
    },
    computed: {
        average() {
            return this.result.reduce((a, c) => a + c, 0) / this.result.length || 0;
        }
    },
    methods: {
        onReset() {
            this.result = [];
        },
        onClickScreen() {
            if (this.state === "waiting") {
                this.state = "ready";
                this.message = "click! If the screen color with green."
                timeout = setTimeout(() => {
                    this.state = "now";
                    this.message = "click!";
                    startTime = new Date();
                }, Math.floor(Math.random() * 1000) + 2000);
            } else if (this.state === "ready") {
                clearTimeout(timeout);
                this.state = "waiting";
                this.message = "You are so hasty!. click! If the screen color with green";
            } else if (this.state === "now") {
                endTime = new Date();
                this.result.push(endTime - startTime);
                this.state = "waiting";
                this.message = 'start with click!';
            }
        }
    }
}
</script>

<style scoped>
#screen {
    width: 300px;
    height: 200px;
    text-align: center;
    user-select: none;
}
#screen.waiting {
    background-color: aqua;

}
#screen.ready {
    background-color: red;
    color: white;
}
#screen.now {
    background-color: greenyellow;
}
</style>