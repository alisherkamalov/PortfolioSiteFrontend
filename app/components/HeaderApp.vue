<template>
    <!-- Оборачиваем весь контент в один корневой элемент -->
    <div class="main">
        <nav>
            <ul>
                <li>
                    <v-card height="35px" class="card author">
                        <v-card-text class="card-text">Alex Portfolio</v-card-text>
                    </v-card>
                </li>
                <li>
                    <v-btn class="btn theme" target="_blank" @click="toggleTheme()">
                        <v-icon class="icon">mdi-white-balance-sunny</v-icon>
                    </v-btn>
                    <v-btn class="btn github" href="https://github.com/alisherkamalov" target="_blank">
                        <v-icon class="icon">mdi-github</v-icon>
                    </v-btn>
                </li>
            </ul>
        </nav>
        <v-row class="img-container">
            <img src="../assets/bgphoto.jpg"></img>
            <div class="blackbg"></div>
            <div class="shadowbg"></div>
            <v-card class="infoo">
                <v-card-text class="conttext">
                    I am a developer specializing in creating {{ text }} websites.
                </v-card-text>
                <v-card-text>
                    <v-btn class="btn-next">Next</v-btn>
                </v-card-text>
            </v-card>
        </v-row>

    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useTheme } from 'vuetify'

const theme = useTheme()

function toggleTheme() {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
}
const text = ref('');

// Тексты для анимации
const texts = ['quickly', 'qualitatively'];

// Функция для набора текста
const typeText = (str, speed, callback) => {
    let index = 0;
    const interval = setInterval(() => {
        text.value += str[index];
        index++;
        if (index === str.length) {
            clearInterval(interval);
            setTimeout(callback, 3000); // 3 секунды задержки перед удалением
        }
    }, speed);
};

// Функция для удаления текста
const deleteText = (speed, callback) => {
    let index = text.value.length;
    const interval = setInterval(() => {
        text.value = text.value.slice(0, index - 1);
        index--;
        if (index === 0) {
            clearInterval(interval);
            setTimeout(callback, 500); // 0.5 секунда задержки перед набором следующего текста
        }
    }, speed);
};

// Функция для запуска анимации
const animateText = () => {
    let textIndex = 0;

    const cycleText = () => {
        typeText(texts[textIndex], 100, () => {
            deleteText(100, () => {
                textIndex = (textIndex + 1) % texts.length; // Переключаемся между текстами
                cycleText();
            });
        });
    };

    cycleText();
};

// Запуск анимации только на клиенте
onMounted(() => {
    animateText();
});
</script>

<style scoped>
ul {
    width: 100%;
    display: flex;
    padding: 0 !important;
    justify-content: space-between;
    list-style-type: none;
    background-color: transparent;
    z-index: 4;
    position: relative;
}

li {
    margin: 15px;
    display: flex;
    gap: 15px;
}

.main {
    height: 100%;
    min-width: 100%;
}

.card {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #282c34;
}

.card.author {
    display: none;
}

.card-text {
    color: white !important;
    font-size: 15px;
    font-weight: 400;
}

.btn {
    border-radius: 100%;
    min-width: 35px !important;
    padding: 0 !important;
    background-color: #282c34 !important;
}

.icon {
    color: white !important;
}

img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.img-container {
    padding: 0;
    margin: 0;
    z-index: 0;
    position: relative;
    overflow: hidden;
    display: flex;
    justify-content: center;
    translate: 0px -70px;
    min-width: 100%;
}

nav {
    z-index: 5;
}



span {
    color: white;
    font-size: 100px !important;
}

.infoo {
    position: absolute;
    top: 150px;
    display: flex;
    z-index: 4;
    font-size: 60px;
    background-color: transparent;
    align-items: center;
    flex-direction: column;
    min-width: 100%;
}

.conttext {
    display: flex;
    font-weight: 100 !important;
    justify-content: center;
    text-align: center;
    line-height: 50px !important;
}

.blackbg {
    z-index: 1;
    background-color: black;
    opacity: 0.6;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
}

.shadowbg {
    z-index: 2;
    background-color: transparent;
    opacity: 1;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    -webkit-box-shadow: 0px -17px 13px -3px rgba(0, 0, 0, 1) inset;
    -moz-box-shadow: 0px -17px 13px -3px rgba(0, 0, 0, 1) inset;
    box-shadow: 0px -17px 13px -3px rgba(0, 0, 0, 1) inset;
}

.btn-next {
    display: none;
}

@media (max-width: 800px) {
    .img-container {
        height: 667px;
    }

    .infoo {
        font-size: 30px;
        max-width: 80% !important;
    }
}

@media (max-width: 1130px) {
    .conttext {
        font-size: 50px !important;
        max-width: 80% !important;
        line-height: 25px;
    }
}

@media (max-width: 1030px) {
    .conttext {
        font-size: 30px !important;
        max-width: 70% !important;
        line-height: 40px !important;
        font-weight: 200;
    }

    .img-container {
        height: 467px;
    }
}


@media (max-width: 500px) {
    .img-container {
        height: 100%;
    }
    .infoo {
        translate: 0px 155px;
    }
    .conttext {
        font-size: 30px !important;
        max-width: 90% !important;
        height: 150px;
    }

    .btn-next {
        display: flex;
    }
}
@media (max-width: 400px) { 
    .conttext {
        height: 200px;
    }
}
@media (min-width: 1130px) {
    .conttext {
        translate: 0px 15px;
        font-size: 50px !important;
        max-width: 80% !important;
        line-height: 25px;
    }

    .img-container {
        height: 667px;
    }
}
</style>