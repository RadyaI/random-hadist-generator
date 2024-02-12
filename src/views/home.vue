<template>
    <div>
        <div class="container">
            <div class="title">
                <h1 class="title-text">Random Hadist Generator</h1>
            </div>
            <div class="center">
                <div class="wrapper" v-if="hadist.book">
                    <div class="book">{{ hadist.book }}</div>
                    <div class="hadist">{{ hadist.hadith_english }}</div>
                    <div class="refno">{{ hadist.refno }}</div>
                </div>
            </div>
            <div class="center">
                <button class="generate-btn" @click="generateHadist">Random Hadist</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';


export default {
    name: 'app',
    data() {
        return {
            hadist: {}
        }
    },
    methods: {
        generateHadist() {
            try {
                axios.get('https://random-hadith-generator.vercel.app/bukhari/')
                    .then(
                        (response) => {
                            console.log(response)
                            this.hadist = response.data.data
                        }
                    )
            } catch (r) {
                console.log(r)
            }
        }
    }
}
</script>

<style scoped>
* {
    font-family: Arial, Helvetica, sans-serif;
}

.container {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: #190482;
}

.title {
    /* border: 1px solid yellow; */
    width: 100%;
    height: auto;
    text-align: center;
    margin-top: 20px;
    color: #C2D9FF;
}

.wrapper {
    /* border: 1px solid red; */
    width: 80%;
    height: 70vh;
    margin-top: 30px;
    background-color: #C2D9FF;
    border-radius: 20px;
    display: flex;
    align-items: center;
    /* justify-content: space-evenly; */
    justify-content: center;
    flex-direction: column;
    color: #190482;
    overflow-x: auto;
}

.book {
    /* border: 1px solid red; */
    width: 70%;
    height: auto;
    font-weight: bolder;
}

.hadist {
    /* border: 1px solid red; */
    width: 70%;
    height: auto;
    margin-top: 20px;
    margin-bottom: 20px;
}

.refno {
    /* border: 1px solid red; */
    width: 70%;
    height: auto;
    font-weight: bolder;
}

.generate-btn {
    margin-top: 40px;
    border: none;
    padding: 10px 70px;
    border-radius: 10px;
    font-weight: bolder;
    background-color: #C2D9FF;
    color: #190482;
    font-size: 1.2rem;
    cursor: pointer;
    position: fixed;
    bottom: 20px;
    border: 2px solid #190482;
}

.center {
    display: flex;
    justify-content: center;
}
</style>