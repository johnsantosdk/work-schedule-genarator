<template>
    <div class="row">
        <div class="col">     
            <button class="btn-mes-anterior btn btn-outline-secondary" >{{ monthsTest[currentMonth-1][0] }}</button>
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
            <select  class="form-control" v-model="currentMonth"> 
                <option  v-for="month in monthsTest" :key="month[0][3]" :value="month[2]">{{month[0]}}</option>
            </select>
        </div>
        <div class="col-sm-1 input-group">
            <select  class="form-control">
                <option value="01">2020</option>
                <option value="02">2021</option>
                <option value="03">2022</option>
            </select>
        </div>    
        <div class="col">
            <button class="btn-mes-posterior btn btn-outline-secondary" >{{ monthsTest[currentMonth+1][0] }}</button>
        </div>  
  {{  monthsTest[0][0] + "----" + fullDate}}
    </div>
</template>

<script>
export default {
    data() {
        return {
            fullDate: (new Date()).toUTCString(),
            monthsTest: [
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
            // months: {
            //     janeiro:'0',
            //     fevereiro:'1',
            //     março:'2',
            //     abril:'3',
            //     maio:'4',
            //     junho:'5',
            //     julho:'6',
            //     agosto:'7',
            //     setembro:'8',
            //     outubro:'9',
            //     novembro:'10',
            //     dezembro:'11'
            //     },
            currentMonth: new Date().getMonth(),
            currentYear: new Date().getFullYear()
        } 
    },
    methods: {
        setDate() {
            const dt = new Date(this.fullDate)
            // const dtt = new Date("2020-02-12")
            console.log('current date: ',this.currentMonth)
            const date = {
                fullDate: dt,
                day: dt.getDate() + 1,
                month: dt.getMonth(),
                year: dt.getFullYear()
            }
            this.$store.state.date = date
            
            console.log(date)
        }
    },
    created() {
        console.log()
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