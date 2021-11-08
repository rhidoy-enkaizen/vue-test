<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png">
        <DatePicker @onSelect="onSelect($event)"/>
        <DatePicker :dateTime="dateTime" :disabled="true"/>
    </div>
</template>

<script>
    import DatePicker from './components/DatePicker.vue'

    export default {
        name: 'App',
        components: {
            DatePicker
        },
        data() {
            return {
                dateTime: ''
            };
        },
        methods: {
            onSelect(dateTime) {
                this.dateTime = dateTime;
            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
