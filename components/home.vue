<script setup>

const counter = useState('counter', () => 100);
const roundedBtnRange = ref(0);
const colorBtnInput = ref('#023b59');
const textColorBtnInput = ref('#f6ebf4');

const primaryButton = reactive({
    backgroundColor: colorBtnInput,
    color: textColorBtnInput,
    border: 'none',
    padding: '0.75rem 1rem',
    cursor: 'pointer',
    borderRadius: computed(() => (roundedBtnRange.value / 10) + 'rem')
})

const kebabize = str => {
    return str.split('').map((letter, idx) => {
        return letter.toUpperCase() === letter
            ? `${idx !== 0 ? '-' : ''}${letter.toLowerCase()}`
            : letter;
    }).join('');
}

/*
function switchRounded() {
    if (roundedBtnInput.value === true) {
        primaryBtnRounded.value = '0.5rem';
    } else {
        primaryBtnRounded.value = '0rem';
    }
}
*/
</script>

<template>
    <div class="flex-middle">
        <div class="style-group">
            <h3>Type</h3>
            <div class="input-flex m1-t">
                <label>
                    <input type="radio" name="btnType">
                    Primary
                </label>
                <label>
                    <input type="radio" name="btnType">
                    Secondary
                </label>
                <label>
                    <input type="radio" name="btnType">
                    Link
                </label>
            </div>
        </div>
        <div class="style-group">
            <h3>Colors</h3>
            <div class="input-flex">
                <label for="colorpicker">
                    <p>Background Color:</p>
                </label>
                <input v-model="colorBtnInput" type="color">
            </div>
            <div class="input-flex">
                <label for="colorpicker">
                    <p>Text Color:</p>
                </label>
                <input v-model="textColorBtnInput" type="color">
            </div>
        </div>
        <div class="style-group">
            <h3>Styles </h3>
            <div class="input-flex">
                <span>Rounded:</span>
                <!--
                <label class="switch">
                    <input type="checkbox" @change="switchRounded()" v-model="roundedBtnInput">
                    <span class="slider round"></span>
                </label>
                -->
                <div>
                    <input v-model="roundedBtnRange" class="range-slider" type="range" min="1" max="30">
                </div>
            </div>
        </div>
        <div>
            <button :style="primaryButton" class="primary-button">
                Primary
            </button>
        </div>
        <div class="code-snippet">
            <p class="link-color">.primary-button {
            <div v-for="(value, key) in primaryButton">
                <span class="m1-l"><span class="primary-color">{{ kebabize(key) }}</span> : <span
                        class="secondary-color">{{
                        value}};</span></span>
            </div>
            <p>}</p>
            </p>
        </div>
    </div>
</template>
  
<style>
.code-snippet {
    background-image: linear-gradient(rgb(0 0 0/20%) 0 0);
    padding: 2rem;
    border-radius: 0.5rem;
}

/*
.primary-button {
    background-color: var(--primary-color);
    border: 1px solid black;
    padding: 0.75rem 1rem;
    cursor: pointer;
    border-radius: 1rem;
}
*/
</style>