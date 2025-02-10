<template>

    <div class="container-fluid bg-success text-center">
        <div class="row">
            <div class="col p-4">

                <!-- title -->
                <h1 class="fs-1 fw-bold">Game | {{ round }}</h1>

            </div>
        </div>
    </div>

</template>

<script>

export default {

    //name component
    name: "HeaderGame",

    props: {

        //props count round
        round: {
            type: String,
            required: true,
            default: "0"
        }
    },

    setup(props) {


        return {

        }

    }
}

</script>