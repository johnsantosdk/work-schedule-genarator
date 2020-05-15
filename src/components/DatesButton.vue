<template>
    <div class="row">
        <div class="col">     
            <button class="btn-mes-anterior btn btn-outline-secondary" >{{ previousMonth }}</button>
        </div>
        <div class="col-sm-1 input-group">
            <select  class="form-control" v-model="currentMonth" @change="setDate()"> 
                <option  v-for="month in months" :key="month[2]" :value="month[2]">{{month[0]}}</option>
            </select>
        </div>
        <div class="col-sm-1 input-group">
            <select  class="form-control" v-model="currentYear" @change="setDate()">
                <option v-for="year in years" :key="year" :value="year">{{ year }}</option>
            </select>
        </div> 
        <div class="col">
            <button class="btn-mes-posterior btn btn-outline-secondary " >{{ nextMonth }}</button>
        </div>  
  
    </div>
</template>

<script>
export default {
    data() {
        return {
            currentFullDate: (new Date()).toUTCString(),
            months: [
                ['janeiro', 'jan','0', '1'],
                ['fevereiro', 'fev','1', '2'],
                ['março', 'mar','2', '3'],
                ['abril', 'abr','3', '4'],
                ['maio', 'mai','4', '5'],
                ['junho', 'jun','5', '6'],
                ['julho', 'jul','6', '7'],
                ['agosto', 'ago','7', '8'],
                ['setembro', 'set','8', '9'],
                ['outubro', 'out','9', '10'],
                ['novembro', 'nov','10', '11'],
                ['dezembro', 'dez','11', '12']
            ],
            monthsName: [
                'janeiro',
                'fevereiro',
                'março',
                'abril',
                'maio',
                'junho',
                'julho',
                'agosto',
                'setembro',
                'outubro',
                'novembro',
                'dezembro',
            ],
            years: ['2020', '2021', '2022', '2023', '2024', '2025', '2026', '2027', '2028', '2029', '2030'], 
            currentMonth: Number(new Date().getMonth()),
            currentYear: new Date().getFullYear() 
        } 
    },
    computed: {
        previousMonth() {
            let p = Number(this.currentMonth) == 0 ? 11 : Number(this.currentMonth) - 1
            return this.monthsName[p]
            
        },
        nextMonth() {
            let n = Number(this.currentMonth) == 11 ? 0 : Number(this.currentMonth) + 1
            return this.monthsName[n]
        }
    },
    methods: {
        setDate() {
            const dt = new Date(this.currentYear, this.currentMonth, (new Date()).getDate())
            const date = {
                currentFullDate: dt,
                day: dt.getDate() + 1,
                month: dt.getMonth(),
                year: dt.getFullYear()
            }
            this.$store.state.date = date
        }

    },
    created() {
        // this.setDate()
    }
}
</script>

<style>

input.input-date {
    width: 145px;
    display: block;
    margin-right: auto;
    margin-left: auto;
}

button.btn-mes-anterior {
    margin-bottom: 15px;
    display: block;
    margin-right: auto;
}

button.btn-mes-posterior {
    margin-bottom: 15px;
    display: block;
    margin-left: auto;
}
</style>