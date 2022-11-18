<script setup>
import ButtonComp from './tabs/button.vue';
const tab = ref(resolveComponent('tabsDefault'));

</script>
<template>
    <div class="flex-horizontal">
        <div style="z-index:1" class="flex-vertical menu-wrapper">
            <div>
                <h3 class="menu-title">
                    Helpers
                </h3>
            </div>
            <button @click="tab = 'layout'" class="menu-item btn-link">
                <p>Layout
                </p>
                <span class="material-symbols-outlined menu-icon">
                    chevron_right
                </span>
            </button>
            <button @click="tab = 'colors'" class="menu-item btn-link">
                <p>Colors
                </p>
                <span class="material-symbols-outlined menu-icon">
                    chevron_right
                </span>
            </button>
            <div>
                <h3 class="menu-title">
                    Components
                </h3>
            </div>
            <button @click="tab = ButtonComp" class="menu-item btn-link">
                <p>Buttons
                </p>
                <span class="material-symbols-outlined menu-icon">
                    chevron_right
                </span>
            </button>
            <button @click="tab = 'headers'" class="menu-item btn-link">
                <p>Headers
                </p>
                <span class="material-symbols-outlined menu-icon">
                    chevron_right
                </span>
            </button>
            <button @click="tab = 'cards'" class="menu-item btn-link">
                <p>Cards
                </p>
                <span class="material-symbols-outlined menu-icon">
                    chevron_right
                </span>
            </button>
        </div>
        <div class="flex-grow">
            <component class="h100" :is="tab" />
        </div>
    </div>
</template>
<style>
</style>