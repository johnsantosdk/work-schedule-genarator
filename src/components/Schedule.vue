<template>
        <div class="schedule">
            <h1>Schedule</h1>
            <DatesButton />
            <table class="table table-striped table-dark">
                <thead>
                    <tr>
                        <th scope="col">Matrícula</th>
                        <th class="col">_________________Funcionário_________________</th>
                        <th scope="col" v-for="day in getDaysInMonth(date.month, date.year)" :key="day">{{ day }}</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <th scope="row">2020</th>
                        <th scope="row">Airton Vieira dos Santos</th>
                        <td>SD</td>
                        <td>SD</td>
                        <td>SN</td>
                        <td>**</td>
                        <td>**</td>
                        <td>SD</td>
                        <td>SD</td>
                        <td>SN</td>
                        <td>**</td>
                        <td>**</td>
                        <td>SD</td>
                        <td>SD</td>
                        <td>SN</td>
                        <td>**</td>
                        <td>**</td>
                        <td>SD</td>
                        <td>SD</td>
                        <td>SN</td>
                        <td>**</td>
                        <td>**</td>
                        <td>SD</td>
                        <td>SD</td>
                        <td>SN</td>
                        <td>**</td>
                        <td>**</td>
                        <td>SD</td>
                        <td>SD</td>
                        <td>SN</td>
                        <td>**</td>
                        <td>**</td>
                        <td>SD</td>
                    </tr>
                    <tr v-for="functionary in functionaries" :key="functionary.id">
                        <th scope="row">{{ functionary.register }}</th>
                        <th scope="row">{{ functionary.name }}</th>
                    </tr>
                </tbody>
            </table>
        </div>
</template>

<script>
import DatesButton from './DatesButton.vue';

export default {
    components: {
        DatesButton
    },
    computed: {
        functionaries() {
            return this.$store.state.functionaries
        },
        date() {
            return this.$store.state.date
        }
    },    
    data() {
        return {
            fullDate: '',
            day: '',
            month: '',
            year: ''
        } 
    },
    created() {
        console.log('created 001')
    },
    methods: {
        getDaysInMonth(month, year) {
            let date = new Date(year, month, 1);
            let days = [];
            while (date.getMonth() === month) {
                days.push(date.getDate())
                // days.push(new Date(date));
                date.setDate(date.getDate() + 1);
            }
            return days;
        },
    }

};
</script>

<style>
div.div-grid {
    font-size: 0.8rem ;
    display: flex;
	flex-direction: column;
    padding: 20px;
}
</style>