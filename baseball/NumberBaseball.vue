<template>
    <div>
        <form v-on:submit.prevent="onSubmitForm">
            <input ref="answer" minlength="4" maxlength="4" type="text" v-model="value">
            <button type="submit">Enter</button>
        </form>
        <div>tries: {{tries.length}}</div>
        <div>
            <ul>
                <li v-for="t in tries">
                    <div>{{t.try}}</div>
                    <div>{{t.result}}</div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tries: [],
            value: '',
            result: (Math.floor(Math.random() * 8) + 1).toString()
            + (Math.floor(Math.random() * 8) + 1).toString()
            + (Math.floor(Math.random() * 8) + 1).toString()
            + (Math.floor(Math.random() * 8) + 1).toString()
        }
    },
    methods: {
        onSubmitForm(e) {
            e.preventDefault();
            console.log('¡§¥‰¿∫ ', this.result);

            let strike = 0;
            let ball = 0;

            for (var i = 0; i < 4; ++i) {
                for (var j = 0; j < 4; ++j) {
                    if (this.value[i] === this.result[j]) {
                        if (i === j) {
                            console.log('i',i,'j',j);
                            strike++;
                        } else {
                            ball++;
                        }
                        break;
                    }
                }
            }

            this.tries.push({
                try: this.value,
                result: 'strike:' + strike + ', ball:' + ball,
            });
            this.value = '';
            this.$refs.answer.focus();
        }
    }
}
</script>