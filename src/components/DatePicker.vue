<template>
    <div>
        <div>
            <span v-show="message">Please select {{ message }}</span>
        </div>
        <select v-model="day" @change="onChange($event)">
            <option disabled value="">Select Day</option>
            <option v-for="n in 31" :key="n">{{n}}</option>
        </select>
        <select v-model="month" @change="onChange($event)">
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
        <select v-model="year" @change="onChange($event)">
            <option disabled value="">Select Year</option>
            <option v-for="year in years" :key="year">{{year}}</option>
        </select>
    </div>
</template>

<script>
    export default {
        name: "DatePicker",
        props: {
            dateTime: String
        },
        watch: {
            dateTime: function (newVal) { // watch it
                //remove message
                this.message = '';
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
                message: '',
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
                if (!this.day)
                    this.message = 'day';
                else if (!this.month)
                    this.message = 'month';
                else if (!this.year)
                    this.message = 'year';
                else {
                    this.message = '';
                    //format day time
                    const dateTime = this.day + ' ' + this.month + ' ' + this.year;
                    this.$emit('onSelect', dateTime)
                }
            }
        }
    }

</script>

<style scoped>

</style>
