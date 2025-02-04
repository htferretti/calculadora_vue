<script setup>
    import { reactive } from 'vue'

    const props = defineProps(['teste'])

    const state = reactive({
        num1: 0,
        num2: 0,
        operation: '',
        result: null,
        operationWord: '',
    })

    function operate() {
        const { num1, num2, operation } = state

        let result
        switch (operation) {
            case 'adicao':
                result = num1 + num2
                state.operationWord = 'adição'
                break
            case 'subtracao':
                result = num1 - num2
                state.operationWord = 'subtração'
                break
            case 'multiplicacao':
                result = num1 * num2
                state.operationWord = 'multiplicação'
                break
            case 'divisao':
                result = num2 !== 0 ? num1 / num2 : 'Erro: divisão por zero'
                state.operationWord = 'divisão'
                break
        }

        state.result = result
    }
</script>

<template>
    <form @change="operate" @submit.prevent="">
        <div class="row mt-5">
            <div class="col-4">
                <input v-model.number="state.num1" required type="number" placeholder="1 número" class="form-control">
            </div>
            <div class="col-4">
                <input v-model.number="state.num2" required type="number" placeholder="2 número" class="form-control">
            </div>
            <div class="col-4">
                <select v-model="state.operation"  class="form-control">
                    <option value="adicao">adição</option>
                    <option value="subtracao">subtração</option>
                    <option value="multiplicacao">multiplicação</option>
                    <option value="divisao">divisão</option>
                </select>
            </div>
        </div>
        <div class="row mt-4">
            <div class="col-12 bg-light py-5 px-4 rounded-5">
                <span class="align-middle">O resultado da {{ state.operationWord }} é: {{ state.result }}</span>
            </div>
        </div>
    </form>
</template>