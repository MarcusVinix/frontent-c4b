<template>
    <div class="radio-input" v-on:click="clicked()">
        <input
            class="checkbox-radio"
            type="radio"
            :id="id"
            :name="name"
            :value="id"
            :checked="isChecked"
        />
        <label class="label-radio" :for="id">{{ label }}</label>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    props: {
        label: String,
        id: String,
        name: String,
        value: [String, Number],
        isChecked: Boolean,
    },
    emits: ['radioClicked'],
    setup(props, context) {
        const clicked = (): void => {
            context.emit('radioClicked')
        }
        return {
            clicked,
        }
    },
})
</script>

<style scoped>
.label-radio {
    background-color: #b29475;
    color: white;
    padding: 6px 16px;
    margin: 10px;
    width: 100%;
    text-align: center;
    border-radius: 15px;
    cursor: pointer;
	white-space: nowrap;
}
.checkbox-radio {
    position: absolute;
    opacity: 0;
    cursor: pointer;
    height: 0;
    width: 0;
}
.radio-input input:checked + .label-radio {
    background-color: #64380c;
}
</style>