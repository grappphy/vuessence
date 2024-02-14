<template>
    <div class="vs-menu" :data-vs-placement="placement">
        <!-- 헤더 -->
        <slot name="header" :default-class="'vs-menu-header'" />

        <!-- 바디 -->
        <slot name="body" :default-class="'vs-menu-body'" :list-class="'vs-menu-list'">
            <div class="vs-menu-body">
                <!-- 슬롯: 리스트 -->
                <slot name="list" :default-class="'vs-menu-list'" />
            </div>
        </slot>

        <!-- 푸터 -->
        <slot name="footer" :default-class="'vs-menu-footer'" />
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "vs-el-menu",
    props: {
        /**
         * 배치
         *
         * @type {String}
         */
        placement: {
            type: String
        }
    }
});
</script>
