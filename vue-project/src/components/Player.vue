<template>

    <!-- section player -->
    <section class="container-fluid mt-5">
        <div class="row justify-content-center px-3 px-sm-0">
            <div class="col-12 col-sm-6 border border-white shadow-lg py-3 text-center">

                <!-- title -->
                <h2 class="fs-5 fw-bold">{{ title }}</h2>

                <!-- healthbar-->
                <div>
                    <div class="progress" role="progressbar" aria-label="Basic example" aria-valuenow="100"
                        aria-valuemin="0" aria-valuemax="100">
                        <div class="progress-bar bg-danger" style="width: 100%;"></div>
                    </div>
                </div>

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
            default: "Player Name"
        }
    },

    setup(props) {


        return {

        }

    }

}

</script>