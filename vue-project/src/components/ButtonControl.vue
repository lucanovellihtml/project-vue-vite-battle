<template>
    <button type="button" :class="classes" :disabled="disabled">{{ title }}</button>
</template>


<script>
import { ref, onMounted } from "vue"

export default {

    props: {

        //props title
        title: {
            type: String,
            required: true,
            default: "Title button"
        },

        //props color with validator name value
        color: {
            type: String,
            required: true,
            validator(value) {
                return ["primary", "danger", "success"].includes(value);
            }
        },

        //props disabled
        disabled: {
            type: Boolean,
            required: false
        }

    },

    emits: ["click-button"],

    setup(props, ctx) {

        //variable class custom
        const classes = ref("");

        //check if button is into DOM
        onMounted(() => {

            //check if color has value and adds custom class
            switch (props.color) {
                case "danger":
                    classes.value = "w-100 btn btn-danger";
                    break;
                case "success":
                    classes.value = "w-100 btn btn-success";
                    break;
                default: classes.value = "w-100 btn btn-primary";
                    break;
            }

        })

        return {
            classes
        }

    }

}

const count = ref(0);

</script>