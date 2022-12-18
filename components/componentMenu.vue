<script setup>
const tabDefault = shallowRef(resolveComponent("tabsDefault"));
const ColorComp = shallowRef(resolveComponent("tabsColor"));
const ButtonComp = shallowRef(resolveComponent("tabsButton"));
const tab = tabDefault;

const styleList = reactive({});

function addStyles(key, name, value, action) {
  if (action === "add") {
    if (name === "" || !/^[a-zA-Z0-9-]+$/.test(name)) {
      alert("pls enter a valid name");
      return;
    }
    if (key === "colors") {
      if (!name.startsWith("--")) {
        alert("Color name must start with '--'");
        return;
      }
    }
    if (!Object.hasOwn(styleList, key)) {
      styleList[key] = new Map();
    }
    if (styleList[key].has(name)) {
      alert("A color with this name already exists.");
    }
    styleList[key].set(name, value);
    return;
  }
  if (action === "delete") {
    styleList[key].delete(name);
    return;
  }
}
</script>
<template>
  <div class="flex-horizontal">
    <div style="z-index: 1" class="flex-vertical menu-wrapper">
      <div>
        <h3 class="menu-title">Helpers</h3>
      </div>
      <button @click="tab = 'layout'" class="menu-item btn-link">
        <p>Layout</p>
        <span class="material-symbols-outlined menu-icon"> chevron_right </span>
      </button>
      <button @click="tab = ColorComp" class="menu-item btn-link">
        <p>Colors</p>
        <span class="material-symbols-outlined menu-icon"> chevron_right </span>
      </button>
      <div>
        <h3 class="menu-title">Components</h3>
      </div>
      <button @click="tab = ButtonComp" class="menu-item btn-link">
        <p>Buttons</p>
        <span class="material-symbols-outlined menu-icon"> chevron_right </span>
      </button>
      <button @click="tab = 'headers'" class="menu-item btn-link">
        <p>Headers</p>
        <span class="material-symbols-outlined menu-icon"> chevron_right </span>
      </button>
      <button @click="tab = 'cards'" class="menu-item btn-link">
        <p>Cards</p>
        <span class="material-symbols-outlined menu-icon"> chevron_right </span>
      </button>
    </div>
    <div class="flex-grow">
      <component
        :is="tab"
        @my-add-styles-event="addStyles"
        :styleListProp="styleList"
      />
    </div>
  </div>
</template>
<style></style>
