<template>
    <div v-if="dados">
        <h1>{{ dados.day}}</h1>
    </div>
</template>

<script lang=ts>
import { defineComponent, toRefs, watch } from 'vue';
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

        const {day, month, year} = formData.value || {}



        watch(formData, (newFormData) => {
            // const obj = newFormData
            // console.log(obj?.day)
            if(newFormData) {


                console.log(newFormData.day)
            }
    });
        
        // const dia = formData.value?.day
        // let data = dia
     
        return {
            dados: formData,
            // data
        }


    }
})
</script>