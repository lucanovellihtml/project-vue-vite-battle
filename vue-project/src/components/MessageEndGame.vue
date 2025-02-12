<!-- template winner -->
<template>

    <!-- section winner -->
    <section class="container-fluid mt-3">
        <div class="row justify-content-center px-3 px-sm-0">
            <div class="col-12 col-sm-6 border border-white shadow-lg py-3 text-center">

                <!-- title -->
                <h2 class="fs-5 fw-bold">{{ message }}</h2>

                <!-- button -->
                <button type="button" class="w-50 btn btn-warning" @click="handleClickReset">Reset</button>

            </div>
        </div>
    </section>

</template>

<script>

import { ref } from "vue"


export default {

    //name component
    name: "MessageEndGame",

    props: {

        //props messagge end game
        message: {
            type: String,
            required: true
        }

    },

    //emit event
    emits: ["click-reset"],

    setup(props, ctx) {

        //function refresh page when game is finished
        const handleClickReset = () => {
            ctx.emit("click-reset");
        }

        return {
            handleClickReset
        }

    }

}


</script>