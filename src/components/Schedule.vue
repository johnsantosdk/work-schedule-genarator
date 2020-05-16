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
                    <tr ref="rowTr">
                        <th scope="row">2020</th>
                        <th scope="row">Airton Vieira dos Santos</th>
                        
                        <td v-for="cycle in renderCycle(9)" :key="cycle.id">{{cycle}}</td>
                        
                    </tr>
                    <tr v-for="functionary in functionaries" :key="functionary.id">
                        <th scope="row">{{ functionary.register }}</th>
                        <th scope="row">{{ functionary.name}}</th>
                        <td v-for="cycle in renderCycle(Number(functionary.cycle))" :key="cycle.id">{{cycle}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
</template>

<script>
import DatesButton from './DatesButton.vue';


export default {
    components: {
        DatesButton,
    },
    data() {
        return {
            cycles: [
                    {id:1, cycle: ['M', 'M', 'M', 'M', 'M', 'F'], info:'5x1-M6H -> trabalha 5 dias em jornada de 6 horas no turno matutino e folga 1 dia.'},
                    {id:2, cycle: ['V', 'V', 'V', 'V', 'V', 'F'], info:'5x1-V6H -> trabalha 5 dias em jornada de 6 horas no turno vespertino e folga 1 dia.'},
                    {id:3, cycle: ['D', 'D', 'D', 'D', 'D', 'F', 'F'], info:'5x2-D10H -> trabalha 5 dias em jornada de 10 horas no turno matutino e vespertino e aos finais de semana e feriados, o chamado horário comercial.'},
                    {id:4, cycle: ['M', 'M', 'M', 'M', 'M', 'M', 'F'], info:'6x1-M6H -> trabalha 6 dias em jornada de 6 horas no turno matutino e folga 1 dia, normalmente trabalha de segunda à sábado e folga aos domingos.'},
                    {id:5, cycle: ['V', 'V', 'V', 'V', 'V', 'V', 'F'], info:'6x1-V6H -> trabalha 6 dias em jornada de 6 horas no turno vespertino e folga 1 dia, normalmente trabalha de segunda à sábado e folga aos domingos.'},
                    {id:6, cycle: ['D', 'F'], info:'12X36-D12H -> trabalha o dia todo jornada de 12 horas no turno diurno e folga 36 horas consecutivas.'},
                    {id:7, cycle: ['DN', 'F'], info:'18X36-D12H+N6H -> trabalha o dia todo em jornada de 12 horas e mais  6 horas no turno noturno e folga 36 horas consecutivas.'},
                    {id:8, cycle: ['DN', 'F', 'F'], info:'24X48-D12H+N12H -> trabalha 24 horas consecutivas e folga 48 horas consecutivas.'},
                    {id:9, cycle: ['M', 'M', 'N', 'F', 'F'], info:'24x24-M6H+M6H+N12H -> Trabalha 2 dias no turno matutino em jornada de 6 horas e mais um diurno em jornada de 12 horas, folgando assim 24 horas consecutivos'},
                    {id:10, cycle: ['V', 'V', 'N', 'F', 'F'], info:'24x24-M6H+M6H+N12H -> Trabalha 2 dias no turno vespertino em jornada de 6 horas e mais um diurno em jornada de 12 horas, folgando assim 24 horas consecutivos'}
           ]
        }
    },
    computed: {
        functionaries() {
            return this.$store.state.functionaries
        },
        date() {
            return this.$store.state.date
        }
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
            this.$store.state.date.length = days.length
            return days;
        },
        renderCycle(functionaryCycleId) {
            let id = functionaryCycleId;
            let objCycle = Object;
            this.cycles.forEach( (obj) => {
                if(obj.id == id) {
                    objCycle = obj;
                }
            })
            let lengthCycle =this.$store.state.date.length;//quantidade de dias no mes
            let rp = parseInt(lengthCycle / objCycle.cycle.length);//quantas repeticoes 
            let md = lengthCycle % objCycle.cycle.length;//resto para completar os 28
            let cont = 0;
            let arr = [];
            while(cont < rp) {
                cont++
                objCycle.cycle.forEach( (item) => {
                    arr.push(item)
                })
                
            }
            let i = 0;
            while(md > 0) {
                arr.push(objCycle.cycle[i])
                md--;
                i++;
            }

            console.log(arr) 
            return arr;
              
        }
    },
    created() {

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