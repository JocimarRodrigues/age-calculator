<template>
    <div class="container">
        <form @submit.prevent="onSubmit">
            <div class="form_container">
                <div class="block">
                    <label for="day">
                        Day
                    </label>
                    <input type="number" placeholder="DD" id="day" v-model="formData.day">
                    <small v-if="formError">{{ formError.day }}</small>
                </div>
                <div class="block">
                    <label for="month">
                        Month
                    </label>
                    <input type="number" placeholder="MM" id="month">
                    <small></small>
                </div>
                <div class="block">
                    <label for="year">
                        Year
                    </label>
                    <input type="number" placeholder="YYYY" id="year">
                    <small></small>
                </div>
            </div>
            <div class="submit_block">
                <hr>
                <button  type="submit" class="submit_btn"><img src="../assets/images/icon-arrow.svg" alt="icon"></button>
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

export interface FormData {
    day: number | null,
    month: number | null,
    year: number| null
}



export default defineComponent({
    name: "FormComponent",
    emits: ['form-submit'], // Declare o evento form-submit aqui
    setup(_, {emit}) {
        const formData = ref<FormData>({
            day: null,
            month: 0,
            year: 0
        })

        const formError = ref({
            day: ''
           })

        const onSubmit = () => {

       

           if(formData.value.day && formData.value.month && formData.value.year) {
           formError.value.day = formData.value.day > 1 && formData.value.day < 31 ? '' : 'Precisa ser uma data válida'
           }

           console.log(formError.value.day)

   

           emit('form-submit', formData.value)
        }
        return {
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