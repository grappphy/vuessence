<template>
    <div class="vs-menu-item">
        <slot />
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "vs-el-menu-item"
});
</script>
