<template>
    <div>
        <!--        <div v-show="errors" class="alert alert-danger" role="alert">-->
        <!--            Please select {{ message }}-->
        <!--        </div>-->
        <div v-if="errors.length">
            <b>Please correct the following error(s):</b>
            <ul>
                <li v-for="error in errors" :key="error">{{error}}</li>
            </ul>
        </div>
        <label for="day">Day</label>
        <select id="day" v-model="day" @change="onChange($event)" :disabled="disabled">
            <option disabled value="">Select Day</option>
            <option v-for="n in 31" :key="n">{{n}}</option>
        </select>
        <label for="month">Day</label>
        <select id="month" v-model="month" @change="onChange($event)" :disabled="disabled">
            <option disabled value="">Select Month</option>
            <option>January</option>
            <option>February</option>
            <option>March</option>
            <option>April</option>
            <option>May</option>
            <option>June</option>
            <option>July</option>
            <option>August</option>
            <option>September</option>
            <option>October</option>
            <option>November</option>
            <option>December</option>
        </select>
        <label for="year">Day</label>
        <select id="year" v-model="year" @change="onChange($event)" :disabled="disabled">
            <option disabled value="">Select Year</option>
            <option v-for="year in years" :key="year">{{year}}</option>
        </select>
    </div>
</template>

<script>
    export default {
        name: "DatePicker",
        props: {
            dateTime: String,
            disabled: Boolean
        },
        watch: {
            dateTime: function (newVal) { // watch it
                //remove message
                this.errors = [];
                //set data
                const array = newVal.split(' ');
                this.day = array[0];
                this.month = array[1];
                this.year = array[2];
            }
        },
        data() {
            return {
                day: '',
                month: '',
                year: '',
                errors: [],
                years: []
            };
        },
        mounted() {
            const yr = new Date().getFullYear();
            for (let i = 11; i > 0; i--) {
                this.years.push(yr - i);
            }
            this.years.push(yr);
            for (let i = 1; i < 11; i++) {
                this.years.push(yr + i);
            }
        },
        methods: {
            onChange() {
                this.errors = [];
                if (this.day && this.month && this.year) {
                    //format day time
                    const dateTime = this.day + ' ' + this.month + ' ' + this.year;
                    this.$emit('onSelect', dateTime)
                    return;
                }
                if (!this.day)
                    this.errors.push('Day field required.');
                if (!this.month)
                    this.errors.push('Month field required.');
                if (!this.year)
                    this.errors.push('Year field required.');
            }
        }
    }

</script>

<style scoped>

</style>
