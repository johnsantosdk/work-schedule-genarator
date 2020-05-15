<template>
    <div class="row">
        <div class="col">     
            <button class="btn-mes-anterior btn btn-outline-secondary" >{{ previousMonth }}</button>
        </div>
        <!-- <div class="col div-align-content-center" >
            <input type="date" class="form-control input-date" v-model="fullDate"><button>Data</button>{{ fullDate }}
        </div> -->
        <!-- <div class="col-sm-2 input-group mb-3">
            <input type="date" class="form-control input-date" v-model="fullDate" value="2020-03-12">
            <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" @click="setDate()">Button</button>
            </div>
        </div> -->
        <div class="col-sm-1 input-group">
            <select  class="form-control" v-model="currentMonth" > 
                <option  v-for="month in months" :key="month[2]" :value="month[2]">{{month[0]}}</option>
            </select>
        </div>
        <div class="col-sm-1 input-group">
            <select  class="form-control">
                <option value="01">2020</option>
                <option value="02">2021</option>
                <option value="03">2022</option>
            </select>
        </div> 
        {{  currentMonth === undefined ? ' nao existe' : '  existe' }}

        <div class="col">
            <button class="btn-mes-posterior btn btn-outline-secondary " >{{ nextMonth }}</button>
        </div>  
  
    </div>
</template>

<script>
export default {
    data() {
        return {
            fullDate: (new Date()).toUTCString(),
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
            monthsTest: [
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
            currentMonth: Number(new Date().getMonth()),
            updateMonth: '',
            currentYear: new Date().getFullYear() 
        } 
    },
    computed: {
        previousMonth() {
            let p = Number(this.currentMonth) == 0 ? 11 : Number(this.currentMonth) - 1
            return this.monthsTest[p]
            
        },
        nextMonth() {
            let n = Number(this.currentMonth) == 11 ? 0 : Number(this.currentMonth) + 1
            return this.monthsTest[n]
        }
    },
    methods: {
        setDate() {
            const dt = new Date(this.fullDate)
            const date = {
                fullDate: dt,
                day: dt.getDate() + 1,
                month: dt.getMonth(),
                year: dt.getFullYear()
            }
            this.$store.state.date = date
        }

    },
    created() {
        // console.log(this.currentMonth)
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