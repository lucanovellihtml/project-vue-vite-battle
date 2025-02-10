<template>

    <section class="container-fluid mt-5" id="log">
        <div class="row justify-content-center px-3 px-sm-0">
            <div class="col-12 col-sm-6 border border-white shadow-lg py-3 text-center">

                <!-- title -->
                <h2 class="fs-5 fw-bold">{{ title }}</h2>

            </div>
        </div>
    </section>

</template>

<script>

import { ref } from "vue"

export default {

    props: {
        title: {
            type: String,
            required: true,
            default: "Battle log"
        }
    },

    setup() {


        return {

        }

    }


}

</script>