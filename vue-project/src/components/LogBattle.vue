<template>

    <section class="container-fluid mt-5">
        <div class="row justify-content-center px-3 px-sm-0">
            <div class="col-12 col-sm-6 border border-white shadow-lg py-3 text-center">

                <!-- title -->
                <h2 class="fs-5 fw-bold">{{ title }}</h2>

                <!-- list log -->
                <ul class="list-group list-group-flush">
                    <li class="list-group-item d-flex gap-2 align-items-center" v-for="log in logs">

                        <!-- player -->
                        <span v-if="log.actionBy === 'player'"
                            class="bg-success fw-bold text-light p-2  rounded-pill">You
                        </span>

                        <!-- span enemy -->
                        <span v-else class="fw-bold bg-warning p-2  rounded-pill">Enemy</span>

                        <!-- span attack -->
                        <span v-if="log.actionType === 'attack'" class="fw-bold">

                            attack with

                            <span class="bg-danger-subtle fw-bold text-dark p-2  rounded-pill">{{
                                log.actionValue }}</span>

                        </span>

                        <!-- spansuper attack -->
                        <span v-else-if="log.actionType === 'super attack'" class="fw-bold">
                            super attack with

                            <span class="bg-danger-subtle fw-bold text-dark p-2  rounded-pill">{{
                                log.actionValue }}</span>

                        </span>

                        <!-- span medikit -->
                        <span v-else-if="log.actionType === 'medikit'" class="fw-bold">
                            medicates himself with

                            <span class="bg-danger-subtle fw-bold text-dark p-2  rounded-pill">{{
                                log.actionValue }}</span>

                        </span>

                        <!-- span gamer over -->
                        <span v-else="log.actionType === 'game over'" class="fw-bold">
                            game over

                            <span class="bg-danger-subtle fw-bold text-dark p-2  rounded-pill">{{
                                log.actionValue }}</span>

                        </span>

                    </li>
                </ul>

            </div>
        </div>
    </section>

</template>

<script>

import { ref } from "vue"

export default {

    props: {

        //prop title
        title: {
            type: String,
            required: true,
            default: "Battle log"
        },

        //prop log messagge
        logs: {
            type: Array,
            required: true
        }

    },

    setup() {

        return {

        }

    }


}

</script>