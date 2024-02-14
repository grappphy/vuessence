<template>
    <vs-el-menu-button @on-click="clickHandler" class="vs-dropdown-menu-button">
        <!-- 슬롯: 아이콘 -->
        <slot name="icon" :default-class="'vs-dropdown-menu-button-icon'" />

        <!-- 슬롯: 텍스트 -->
        <slot name="text" :default-class="'vs-dropdown-menu-button-text'" />
    </vs-el-menu-button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

// Elements
import VsElMenuButton from "../menu/el-menu-button.vue";

export default defineComponent({
    name: "vs-el-dropdown-menu-button",
    components: {
        VsElMenuButton
    },
    setup(props, { emit }) {
        // 버튼 클릭
        function clickHandler(): void {
            emit("on-click");
        }

        return {
            clickHandler
        };
    }
});
</script>
