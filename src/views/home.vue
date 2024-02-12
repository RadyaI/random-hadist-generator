<template>
    <div>
        <div class="container">
            <Star v-for="(star, index) in stars" :key="index" :position="star.position" />
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

import Star from '../components/star.vue';

export default {
    name: 'app',
    components: {
        Star
    },
    data() {
        return {
            hadist: {},
            stars: [],
            numberOfStars: 50,
        }
    },
    mounted() {
        this.initializeStars();
        setInterval(this.updateStars, 16);
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
        },
        initializeStars() {
            for (let i = 0; i < this.numberOfStars; i++) {
                this.stars.push({
                    position: {
                        x: Math.random() * window.innerWidth,
                        y: Math.random() * window.innerHeight,
                    },
                });
            }
        },
        resetStarPosition(star) {
            star.position.y = 0;
            star.position.x = Math.random() * window.innerWidth;
        },
        updateStars() {
            for (const star of this.stars) {
                star.position.y += 1;

                if (star.position.y > window.innerHeight) {
                    this.resetStarPosition(star);
                }
            }
        },
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
    background-color: #03001C;
}

.title {
    /* border: 1px solid yellow; */
    width: 100%;
    height: auto;
    text-align: center;
    margin-top: 20px;
    color: #B6EADA;
}

.wrapper {
    /* border: 1px solid red; */
    width: 80%;
    height: fit-content;
    max-height: 70vh;
    margin-top: 30px;
    background-color: #B6EADA;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    color: #03001C;
    overflow-x: auto;
}

.book {
    /* border: 1px solid red; */
    width: 70%;
    height: auto;
    font-weight: bolder;
    padding-top: 60px;
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
    padding-bottom: 60px;
}

.generate-btn {
    margin-top: 40px;
    border: none;
    padding: 10px 70px;
    border-radius: 10px;
    font-weight: bolder;
    background-color: #B6EADA;
    color: #03001C;
    font-size: 1.2rem;
    cursor: pointer;
    position: fixed;
    bottom: 20px;
    border: 2px solid #03001C;
}

.center {
    display: flex;
    justify-content: center;
}
</style>