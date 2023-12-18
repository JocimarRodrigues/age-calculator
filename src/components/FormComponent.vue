<template>
    <div class="container">
        <form @submit.prevent="onSubmit">
            <div class="form_container">
                <div class="block">
                    <label for="day">
                        Day
                    </label>
                    <input type="number" placeholder="DD" id="day" v-model="day" required>
                    <small v-if="formError">{{ formError.day }}</small>
                </div>
                <div class="block">
                    <label for="month">
                        Month
                    </label>
                    <input type="number" placeholder="MM" id="month" v-model="month" required>
                    <small v-if="formError">{{ formError.month }}</small>
                </div>
                <div class="block">
                    <label for="year">
                        Year
                    </label>
                    <input type="number" placeholder="YYYY" id="year" v-model="year" required>
                    <small v-if="formError">{{ formError.year }}</small>
                </div>
            </div>
            <div class="submit_block">
                <hr>
                <button type="submit" class="submit_btn"><img src="../assets/images/icon-arrow.svg" alt="icon"></button>
            </div>
        </form>
        <div class="output">
            <h1><span id="YY">--</span>years</h1>
            <h1><span id="MM">--</span>months</h1>
            <h1><span id="DD">--</span>days</h1>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { IFormData } from '../interfaces/IFormData'
import {IFormError} from '../interfaces/IFormError'

export default defineComponent({
    name: "FormComponent",
    emits: ['form-submit'], // Declare o evento form-submit aqui
    setup(_, { emit }) {
        const formData = ref<IFormData>({
            day: 0,
            month: 0,
            year: 0
        })

        const day = ref<number | null>(null)
        const month = ref<number | null>(null)
        const year = ref<number | null>(null)

        const formError = ref<IFormError>({
            day: '',
            month: '',
            year: ''
        })

        const onSubmit = () => {
            formError.value.day = day.value && day.value >= 1 && day.value <= 31 ? '' : 'Precisa ser uma data válida';
            formError.value.month = month.value && month.value >= 1 && month.value <= 12 ? '' : 'Precisa ser uma data válida';
            formError.value.year = year.value && year.value >= 1 && year.value <= 2023 ? '' : 'Precisa ser uma data válida';

            if (!formError.value.day && !formError.value.month && !formError.value.year) {
                const formData: IFormData = {
                    day: day.value || 0,
                    month: month.value || 0,
                    year: year.value || 0
                };

                emit('form-submit', formData);
            }

        }
        return {
            day,
            month,
            year,
            formData,
            onSubmit,
            formError
        }
    }
})
</script>

<style lang="scss" scoped>
@import '../styles/variables';




.container {
    padding: 2rem;
    display: flex;
    flex-direction: column;

    form {
        display: flex;
        flex-direction: column;

        .form_container {
            display: flex;
            gap: 2rem;

            .block {
                display: flex;
                flex-direction: column;

                label {
                    text-align: left;
                    text-transform: uppercase;
                    font-weight: 600;
                }

                input {
                    width: 100px;
                    padding: .5rem;
                    border-radius: .5rem;
                    border: 1px solid $Light-grey;
                    display: flex;
                    align-items: center;
                    font-size: 1.5rem;

                    &::placeholder {
                        font-size: 1.5rem;
                        font-weight: 800;
                    }
                }
            }


        }

        .submit_block {
            display: flex;
            align-items: center;

            hr {
                width: 100%;
            }


            .submit_btn {
                border-radius: 50%;
                padding: 1rem;
                background-color: $Purple;
                border: none;
                cursor: pointer;
                display: flex;
                align-items: center;
                justify-content: center;
            }


        }

    }

}




.output h1 {
    font-size: 5rem;
    font-weight: 800;
    font-style: italic;
    height: fit-content;
}

.output span {
    color: $Purple;
}

small {
    color: red;
}
</style>