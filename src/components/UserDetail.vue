<template>
    <div class="component">
        <h3>You may view the User Details here</h3>
        <p>Many Details</p>
        <p>User Name: {{ switchName() }}</p>
        <p>User Age: {{ userAge }}</p>
        <button @click="resetName">Reset Name</button>
        <button @click="resetFn()">Reset Name</button>
    </div>
</template>

<script>
    import { eventBus } from '../main.js'

    export default {
        // props validation as object
        props: {
            name: {
                type: String
            },
            resetFn: Function,
            userAge: Number
        },
        methods: {
            switchName() {
                return this.name + ' is awesome'
            },
            resetName() {
                this.name = 'Sean';
                this.$emit('nameWasReset', this.name)
            }
        },
        created() {
            // listen to events emitted ON this Vue instance
            eventBus.$on('ageWasEdited', (age) => {
                this.userAge = age;
            });
        }
    }
</script>

<style scoped>
    div {
        background-color: lightcoral;
    }
</style>
