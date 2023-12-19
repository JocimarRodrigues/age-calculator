<template>
    <div v-if="data" class="output">
        <h1><span id="YY">{{ data.year }}</span>years</h1>
        <h1><span id="MM">{{ data.month }}</span>months</h1>
        <h1><span id="DD">{{ data.day }}</span>days</h1>
    </div>
</template>

<script lang=ts>
import { defineComponent, toRefs, watch, ref } from 'vue';
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

        let data = ref<IFormData>()

        watch(formData, (newFormData) => {

            if (newFormData) {
                const currentDate = new Date()
                const birthDate = new Date(newFormData.year, newFormData.month - 1, newFormData.day);
                const ageInMilliseconds = currentDate.getTime() - birthDate.getTime();
                const ageInDays = Math.floor(ageInMilliseconds / (1000 * 60 * 60 * 24));
                const years = Math.floor(ageInDays / 365);
                const months = Math.floor((ageInDays % 365) / 30.4375);
                const days = Math.floor(ageInDays % 30.4375);

                const result = {
                    day: days,
                    month: months,
                    year: years
                } as IFormData

                data.value = result

            }
        });

        return {
            data

        }


    }
})
</script>

<style scoped lang="scss">
@import '../styles/variables';

.output {
    padding: 2rem;
    h1 {
        font-size: 5rem;
        font-weight: 800;
        font-style: italic;

    }

    span {
        color: $Purple;
    }
}
</style>