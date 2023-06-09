<template>
    <div>
        <input
            v-bind="$attrs"
            class="input-base"
            @input="onInput"
            :modelValue="formattedValue"
            ref="inputRef"
        />
        <div v-show="isInvalid">
            <InputError :msg="errors" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType, watch } from 'vue'
import { useCurrencyInput, CurrencyInputOptions } from 'vue-currency-input'
import InputError from '@/components/ui/InputError.vue'

/**
 * Component utilizado para input numerico de formato 'currency'
 * @prop {Boolean} isInvalid - Condição para verficar se o input é válido
 * @prop {Array<String>} errors - Array de string contendo todos as mensagens 
 * de erros
 * @prop {CurrencyOptions} currencyOptions - Objeto com as configuracoes do 
 * tipo do currency
 * @prop {number} modelValue - value do input
 * @event inputEvent - Evento para quando algo é escrito no input
 */
export default defineComponent({
    components: {
        InputError,
    },
    props: {
        isInvalid: {
            type: Boolean,
            required: true,
        },
        errors: {
            type: Array as PropType<string[]>,
            required: true,
        },
        currencyOptions: {
            type: Object as PropType<CurrencyInputOptions>,
            required: true,
        },
        modelValue: {
            type: Number,
            required: true,
        },
    },
    emits: ['inputEvent'],
    inheritAttrs: false,
    setup(props, context) {
        const { inputRef, formattedValue, setValue } = useCurrencyInput(
            props.currencyOptions
        )
        watch(
            () => props.modelValue,
            (value) => {
                setValue(value)
            }
        )
        /**
         * Função chamada para emitir um evento quando algo é escrito no input
         * @param {any} event - dados do evento recebido pelo input
         */
        function onInput(event: any) {
            context.emit('inputEvent', event.target.value)
        }
        return {
            onInput,
            inputRef,
            formattedValue,
        }
    },
})
</script>

<style scoped>
.input-base {
    max-width: 100%;
    width: calc(100% - 30px);
    padding: 15px;
    font-size: 18px;
    margin: 10px 0;
    border-radius: 5px;
}
.btn-next {
    margin: 40px 20px;
    text-align: right;
}
</style>