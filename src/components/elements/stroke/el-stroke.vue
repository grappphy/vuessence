<template>
    <div class="vs-stroke">
        <svg class="vs-stroke-svg" xmlns="http://www.w3.org/2000/svg">
            <!-- 슬롯: 정의 -->
            <slot name="defs" />

            <!-- 슬롯: 모양 -->
            <slot name="shape" />
        </svg>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "vs-el-stroke"
});
</script>
