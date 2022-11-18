<script setup>

const counter = useState('counter', () => 100);
const roundedBtnRange = ref(0);
const colorBtnInput = ref('#023b59');
const textColorBtnInput = ref('#f6ebf4');
const snippitExpand = ref({open: false, show: 'Show', chevron: 'less' })

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

function toggleCodeSnippet(){
    if(snippitExpand.value.open){
        snippitExpand.value.open = false;
        snippitExpand.value.show = 'Show';
        snippitExpand.value.chevron = 'less';
    }else{
        snippitExpand.value.open = true;
        snippitExpand.value.show = 'Hide';
        snippitExpand.value.chevron = 'More';
    }
}

</script>

<template>
    <div class="flex-horizontal w100">
        <div class="flex-vertical menu-wrapper">
            <div class="style-group">
                <h3 class="menu-title">Type</h3>
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
                <h3 class="menu-title">Colors</h3>
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
                <h3 class="menu-title">Styles </h3>
                <div class="input-flex">
                    <span>Rounded:</span>
                    <div>
                        <input v-model="roundedBtnRange" class="range-slider" type="range" min="1" max="30">
                    </div>
                </div>
            </div>
        </div>
        <div class="main-content flex-middle flex-grow">
            <div>
                <button :style="primaryButton" class="primary-button w100">
                    Primary
                </button>
            </div>
            <div class="code-snippet" :class="{ showcode: snippitExpand.open }">
                <button @click="toggleCodeSnippet()" class="btn-link show-code-btn m1-b">
                    <p> {{snippitExpand.show}} Code <span class="material-symbols-outlined icon-code-snippet">
                            expand_{{snippitExpand.chevron}}
                        </span></p>
                </button>
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
    </div>
</template>
  
<style>
.main-content {
    flex-direction: column;
    justify-content: space-between;
    margin-top: 2rem;
    overflow-y: hidden;
}

.style-group {
    margin: 0.5rem 0;
}

.code-snippet {
    background-image: linear-gradient(rgb(0 0 0/20%) 0 0);
    padding: 1rem 2rem 2rem 2rem;
    width: 100%;
    transform: translateY(calc(100% - 3.5rem));
    transition: all 200ms ease;
}

.showcode {
    transform: translateY(0);
}

.icon-code-snippet {
    font-size: 1.5rem;
    line-height: 0rem;
    transform: translateY(0.4rem);
}

.show-code-btn{
    opacity: 0.9;
    transform: scale(0.9);
}

.show-code-btn:hover{
    opacity: 1;
    transform: scale(1);
    background-color: transparent;
}

</style>