<template>

    <!-- section player -->
    <section class="container-fluid mt-5">
        <div class="row justify-content-center px-3 px-sm-0">
            <div class="col-12 col-sm-6 border border-white shadow-lg py-3 text-center">

                <!-- title -->
                <h2 class="fs-5 fw-bold">{{ title }} : {{ healt }}</h2>

                <!-- healthbar-->
                <div>
                    <div class="progress" role="progressbar" aria-label="Basic example" aria-valuenow="100"
                        aria-valuemin="0" aria-valuemax="100">
                        <div class="progress-bar bg-danger" :style="healthBarStyle"></div>
                    </div>
                </div>

            </div>
        </div>
    </section>


</template>

<script>

import { ref, computed } from "vue"

export default {

    //name component
    name: "Player",

    props: {
        title: {
            type: String,
            required: true,
            default: "Player Name"
        },
        healt: {
            type: Number,
            required: true,
            default: 0
        }
    },

    setup(props) {

        //computed to manipulate health bar
        const healthBarStyle = computed(() => {
            return { width: props.healt + "%" }
        })

        return {
            healthBarStyle
        }

    }

}

</script>