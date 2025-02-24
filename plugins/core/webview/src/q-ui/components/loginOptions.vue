<!-- Copyright 2024 Amazon.com, Inc. or its affiliates. All Rights Reserved. -->
<!-- SPDX-License-Identifier: Apache-2.0 -->

<template>
    <QOptions v-if="app === 'AMAZONQ'" @stageChanged="stageChanged" @login="login" @emitUiClickTelemetry="emitUiClickTelemetry"/>
    <ToolkitOptions v-if="app === 'TOOLKIT'" @stageChanged="stageChanged" @login="login" @emitUiClickTelemetry="emitUiClickTelemetry"/>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import QOptions from "./qOptions.vue";
import ToolkitOptions from "./toolkitOptions.vue"
import {Stage, LoginIdentifier, BuilderId, LoginOption} from "../../model";

export default defineComponent({
    name: "loginOptions",
    components: {
        QOptions,
        ToolkitOptions
    },
    props: {
        app: String
    },
    computed: {},
    data() {
        return {
            app: this.app,
            existingLogin: { id: -1, text: '', title: '' },
            selectedLoginOption: LoginIdentifier.NONE,
            LoginOption: LoginIdentifier
        }
    },
    methods: {
        stageChanged(stage: Stage) {
            this.$emit('stageChanged', stage)
        },
        login(type: LoginOption) {
            this.$emit('login', type)
        },
        emitUiClickTelemetry(elementId: string) {
            this.$emit('emitUiClickTelemetry', elementId)
        }
    }
})
</script>
