<template>
    <div @click="clickHandler" :class="classes">
        <div class="vs-dialog-content">
            <!-- 슬롯: 콘텐츠 이전 -->
            <slot name="content-before" />

            <!-- 패널 -->
            <div class="vs-dialog-panel">
                <!-- 헤더 -->
                <div v-if="useHeader" class="vs-dialog-header">
                    <!-- 슬롯: 헤더 콘텐츠 -->
                    <slot name="header-content">
                        <div class="vs-dialog-header-start">
                            <!-- 슬롯: 헤더 시작 콘텐츠 -->
                            <slot name="header-start-content" :title-class="'vs-dialog-header-title'" />
                        </div>

                        <div class="vs-dialog-header-end">
                            <!-- 슬롯: 헤더 종료 콘텐츠 -->
                            <slot
                                name="header-end-content"
                                :button-class="'vs-dialog-header-button'"
                                :icon-class="'vs-dialog-header-button-icon'"
                            />
                        </div>
                    </slot>
                </div>

                <!-- 바디 -->
                <div class="vs-dialog-body">
                    <!-- 슬롯: 바디 콘텐츠 -->
                    <slot name="body-content">
                        <!-- 바디 시작 -->
                        <div v-if="useBodyStart" class="vs-dialog-body-start">
                            <!-- 슬롯: 바디 시작 콘텐츠 -->
                            <slot name="body-start-content" />
                        </div>

                        <!-- 바디 종료 -->
                        <div class="vs-dialog-body-end">
                            <!-- 슬롯: 바디 시작 종료 -->
                            <slot
                                name="body-end-content"
                                :title-class="'vs-dialog-body-title'"
                                :text-class="'vs-dialog-body-text'"
                            />
                        </div>
                    </slot>
                </div>

                <!-- 푸터 -->
                <div v-if="useFooter" class="vs-dialog-footer">
                    <!-- 슬롯: 푸터 콘텐츠 -->
                    <slot name="footer-content">
                        <vs-el-buttons class="vs-dialog-footer-buttons">
                            <template #item="{ defaultClass }">
                                <slot
                                    name="footer-buttons-content"
                                    :item-class="defaultClass"
                                    :button-class="'vs-dialog-footer-button'"
                                />
                            </template>
                        </vs-el-buttons>
                    </slot>
                </div>
            </div>

            <!-- 슬롯: 콘텐츠 이후 -->
            <slot name="content-after" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, computed } from "vue";

// Elements
import VsElButtons from "../button/el-button.vue";

export default defineComponent({
    name: "vs-el-dialog",
    components: {
        VsElButtons
    },
    props: {
        /**
         * 유형
         *
         * @type {String}
         */
        type: {
            type: String
        },
        /**
         * 크기
         *
         * @type {String}
         */
        size: {
            type: String
        },
        /**
         * 헤더 사용 여부
         *
         * @type {Boolean}
         */
        useHeader: {
            type: Boolean
        },
        /**
         * 바디 시작 사용 여부
         *
         * @type {Boolean}
         */
        useBodyStart: {
            type: Boolean
        },
        /**
         * 푸터 사용 여부
         *
         * @type {Boolean}
         */
        useFooter: {
            type: Boolean
        },
        /**
         * 패딩 없음 사용 여부
         *
         * @type {Boolean}
         */
        usePaddingless: {
            type: Boolean
        },
        /**
         * 푸터 없음 사용 여부
         *
         * @type {Boolean}
         */
        useFooterless: {
            type: Boolean
        }
    },
    setup(props, { emit }) {
        const classes = computed(() => {
            const defaultClass = "vs-dialog";

            const typeClass = props.type ? `${defaultClass}:${props.type}` : null;

            const sizeClass = props.size ? `${defaultClass}{${props.size}}` : null;

            const footerlessClass = props.useFooterless ? `${defaultClass}{footerless}` : "";

            const paddinglessClass = props.usePaddingless ? `${defaultClass}{paddingless}` : "";

            return [defaultClass, typeClass, sizeClass, footerlessClass, paddinglessClass];
        });

        // 클릭
        function clickHandler(event: Event): void {
            emit("vs-on-click", event);
        }

        return {
            classes,

            clickHandler
        };
    }
});
</script>
