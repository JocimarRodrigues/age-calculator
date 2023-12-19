<template>
    <div v-if="data">
        <h1>{{ data.day }}</h1>
        <h1>{{ data.month }}</h1>
    </div>
</template>

<script lang=ts>
import { defineComponent, toRefs, watch,ref } from 'vue';
import { IFormData } from '@/interfaces/IFormData';
export default defineComponent({
    name: 'ResultComponent',
    props: {
        formData: {
            type: Object
        }
    },
    setup(props) {


        const { formData } = toRefs(props) // toRefs para manter reatividade das props

        let data = ref()

        watch(formData, (newFormData) => {

            if (newFormData) {
                const currentDate = new Date()
                const birthDate = new Date(newFormData.year, newFormData.month - 1, newFormData.day); 
                const ageInMilliseconds = currentDate.getTime() - birthDate.getTime();
                const ageInDays = Math.floor(ageInMilliseconds / (1000 * 60 * 60 * 24));

                const years = Math.floor(ageInDays / 365);
                const months = Math.floor((ageInDays % 365) / 30.4375); 
                const days = ageInDays % 30.4375;




                const result = {
                    day: days,
                    month: months,
                    year: years
                }



                data.value = result

            }
        });

        console.log(data)

        // const dia = formData.value?.day
        // let data = dia

        return {
            dados: formData,
            data
            // data
        }


    }
})
</script>