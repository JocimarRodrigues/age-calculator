<template>
    <div>
        <h1>{{ dados.day }}</h1>
    </div>
</template>

<script lang=ts>
import { defineComponent, toRefs } from 'vue';
export default defineComponent({
    name: 'ResultComponent',
    props: {
        formData: {
            type: Object
        }
    },
    setup(props) {

        const { formData } = toRefs(props) // toRefs para manter reatividade das props
        return {
            dados: formData
        }


    }
})
</script>