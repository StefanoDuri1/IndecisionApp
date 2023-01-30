<template>
    <div>
        <img src="" alt="bg-image">
        <div class="bg-dark"></div>

        <div class="indecision-container">
            <input type="text" placeholder="Make me a question" v-model="question">
            <p>Remember to end with a question mark (?) </p>

            <div>
                <h2>{{ question }}</h2>
                <h1>{{ answer }}</h1>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Indecision',
    data() {
        return {
            question: null,
            answer: null
        }
    },
    methods: {
        async getAnswer() {
            this.answer = 'Thinking...'
            
            const url = 'https://yesno.wtf/api'
            const response = await fetch(url)
            const result =  await response.json()
            
            const { answer, image } = result

            this.answer = answer
        }
    },
    watch: {
        question( value, oldValue ) {
            if(!value.includes('?')) return

            this.getAnswer()
        }
    }
}
</script>
<style scoped>
img, .bg-dark {
    height: 100vh;
    left: 0px;
    max-height: 100%;
    max-width: 100%;
    position: fixed;
    top: 0px;
    width: 100vw;
}

.bg-dark {
    background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
    position: relative;
    z-index: 99;
}

input {
    width: 250px;
    padding: 10px 15px;
    border-radius: 5px;
    border: none;
}
input:focus {
    outline: none;
}

p {
    color: white;
    font-size: 20px;
    margin-top: 0px;
}

h1, h2 {
    color: white;
}

h2 {
    margin-top: 150px;
}
</style>