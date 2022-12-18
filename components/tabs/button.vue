<script setup>

const snippitExpand = ref({ open: false, show: 'Show', chevron: 'less' });
const buttonNameInput = ref('');

const buttonList = reactive({});
const selectdBtn = ref('');


function camelToKebab(input) {
    return input.replace(/([a-z])([A-Z])/g, '$1-$2').toLowerCase();
}

function kebabToCamel(input) {
    return input.replace(/-([a-z])/g, function (g) {
        return g[1].toUpperCase();
    });
}

function toggleCodeSnippet() {
    if (snippitExpand.value.open) {
        snippitExpand.value.open = false;
        snippitExpand.value.show = 'Show';
        snippitExpand.value.chevron = 'less';
    } else {
        snippitExpand.value.open = true;
        snippitExpand.value.show = 'Hide';
        snippitExpand.value.chevron = 'More';
    }
}

function createButton() {
    if (buttonNameInput.value === '' || !(/^[a-zA-Z0-9-]+$/.test(buttonNameInput.value))) {
        alert("Please enter a valid name / Names may only contain letters, numbers and -'s");
        return;
    }
    var name = kebabToCamel('btn-' + buttonNameInput.value);
    if (buttonList[name]) {
        alert('A button with this name already exists.');
        return;
    }
    buttonList[name] = {
        backgroundColor: '#4cbfa6',
        color: '#000000',
        border: 'none',
        padding: '0.75rem 1rem',
        cursor: 'pointer',
        borderRadius: '0rem'
    };
    /*const test = computed(() => (roundedBtnRange.value / 10) + 'rem');*/
    selectdBtn.value = camelToKebab(name);
}

function updateBorder(e) {
    buttonList[kebabToCamel(selectdBtn.value)].borderRadius = e.target.value / 10 + 'rem';
}

</script>

<template>
    <div class="flex-horizontal w100">
        <div class="flex-vertical menu-wrapper">
            <div>
                <label for="buttons" class="m1-t">
                    <p>Create New Button</p>
                </label>
                <input class="text-input w100" type="text" placeholder="New Button Name" v-model="buttonNameInput">
                <p class="small">* all buttons will be named 'btn-{name}'</p>
                <button @click="createButton()" class="btn-primary btn-create w100">
                    <p>Create</p>
                </button>
            </div>
            <label for="buttons" class="m1-t">
                <p>Your Buttons:</p>
            </label>
            <select v-model="selectdBtn" name="buttons" required>
                <option value="" disabled>Create or choose a button</option>
                <option v-for="(value, key) in buttonList">{{ camelToKebab(key) }}</option>
            </select>
            <div v-if="selectdBtn">
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
                        <input v-model="buttonList[kebabToCamel(selectdBtn)].backgroundColor" type="color">
                    </div>
                    <div class="input-flex">
                        <label for="colorpicker">
                            <p>Text Color:</p>
                        </label>
                        <input v-model="buttonList[kebabToCamel(selectdBtn)].color" type="color">
                    </div>
                </div>
                <div class="style-group">
                    <h3 class="menu-title">Styles </h3>
                    <div class="input-flex">
                        <span>Rounded:</span>
                        <div>
                            <input @change="updateBorder" value="0" class="range-slider" type="range" min="1" max="20">
                        </div>
                    </div>
                </div>
            </div>
        </div>


        <div class="main-content flex-middle flex-grow">
            <div class="w100">
                <div v-for="(value, key) in buttonList" class="flex-middle"
                    :class="{ 'test': kebabToCamel(selectdBtn) === key }">
                    <button :style="value" class="primary-button m1-tb">
                        {{ camelToKebab(key) }}
                    </button>
                </div>
            </div>

            <div class="code-snippet" :class="{ showcode: snippitExpand.open }">
                <button @click="toggleCodeSnippet()" class="btn-link show-code-btn m1-b">
                    <p> {{ snippitExpand.show }} Code <span class="material-symbols-outlined icon-code-snippet">
                            expand_{{ snippitExpand.chevron }}
                        </span></p>
                </button>

                <p>.<span class="link-color">{{ selectdBtn }}</span> {</p>
                <div v-for="(value, key) in buttonList[kebabToCamel(selectdBtn)]">
                    <span class="m1-l"><span class="primary-color">{{ camelToKebab(key) }}</span>: <span
                            class="secondary-color">{{
                            value}};</span></span>
                </div>
                <p>}</p>
            </div>
        </div>



    </div>
</template>
  
<style>
.test {
    background-color: rgb(0 0 0/25%);
}

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

.show-code-btn {
    opacity: 0.9;
    transform: scale(0.9);
}

.show-code-btn:hover {
    opacity: 1;
    transform: scale(1);
    background-color: transparent;
}

.btn-create {
    margin-top: 0.3rem;
}
</style>