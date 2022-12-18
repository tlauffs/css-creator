<script setup>
const emit = defineEmits(['myAddStylesEvent']);
const currentColor = ref('#ffffff');
const currentName = ref('');

const props = defineProps(['styleListProp']);
const styleList = props.styleListProp;

function addColor() {
    emit("myAddStylesEvent", 'colors', currentName.value, currentColor.value);
}
</script>
<template>
    <div>
        <div>{{ styleList }}</div>
        <div class="flex-vertical main-color-wrapper">
            <h2>Add Colors you want to use on your App</h2>
        </div>
        <div v-for="color in styleList.colors" class="input-flex color-flex" :style="{ backgroundColor: currentColor }">
            <div class="hover-text">
                <p>
                    <span class="material-symbols-outlined">
                        info
                    </span>
                </p>

                <span class="tooltip-text" id="bottom">
                    <p class="m1-b">The enterd name will be the name of your CSS custom property. You will be able to
                        use it
                        anywhere in your webapp and to style components in this tool.</p>
                    <p class="m1-b">Custom property names must start with '--'</p>
                    <p class="m1-b">Typical CSS color variable format: </p>
                    <p class="m1-b"> --{ name }-color<br> exp: --primary-color</p>
                    <p>
                        For more info <a target="_blank"
                            href="https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties">click
                            here.</a>
                    </p>
                </span>
            </div>
            <div class="flex-middle gap">
                <p>color</p>
                <div>
                    <input class="text-input" type="text" v-model="currentName" placeholder="Enter Color Name">
                </div>
                <div>
                    <input type="color" v-model="currentColor">
                </div>
                <button class="btn-white" @click="addColor">
                    <p class="flex-middle">
                        <span class="material-symbols-outlined m1-rs">
                            add
                        </span>Add Color
                    </p>
                </button>
            </div>
        </div>
    </div>
</template>

<style>
.main-color-wrapper {
    padding: 2rem;
}

.color-flex {
    justify-content: center;
    gap: 1rem;
    padding: 2rem 0;
}

.contrast-color {
    filter: invert(1) saturate(0.5);
    transition: all 200ms ease-in-out;
}
</style>