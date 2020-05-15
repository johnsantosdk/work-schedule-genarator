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
                        
                        <td v-for="cycle in cycles.custom[0]._24x24" :key="cycle">{{cycle}}</td>
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
    data() {
        return {
            cycles: {
                standard: [
                    {_5x1:['M', 'M', 'M', 'M', 'M', 'F'], info:'5x1-M6H -> trabalha 5 dias em jornada de 6 horas no turno matutino e folga 1 dia.'},
                    {_5x1:['V', 'V', 'V', 'V', 'V', 'F'], info:'5x1-V6H -> trabalha 5 dias em jornada de 6 horas no turno vespertino e folga 1 dia.'},
                    {_5x2:['D', 'D', 'D', 'D', 'D', 'F', 'F'], info:'5x2-D10H -> trabalha 5 dias em jornada de 10 horas no turno matutino e vespertino e aos finais de semana e feriados, o chamado horário comercial.'},
                    {_6x1:['M', 'M', 'M', 'M', 'M', 'M', 'F'], info:'6x1-M6H -> trabalha 6 dias em jornada de 6 horas no turno matutino e folga 1 dia, normalmente trabalha de segunda à sábado e folga aos domingos.'},
                    {_6x1:['V', 'V', 'V', 'V', 'V', 'V', 'F'], info:'6x1-V6H -> trabalha 6 dias em jornada de 6 horas no turno vespertino e folga 1 dia, normalmente trabalha de segunda à sábado e folga aos domingos.'},
                    {_12X36:['D', 'F'], info:'12X36-D12H -> trabalha o dia todo jornada de 12 horas no turno diurno e folga 36 horas consecutivas.'},
                    {_18X36:['DN', 'F'], info:'18X36-D12H+N6H -> trabalha o dia todo em jornada de 12 horas e mais  6 horas no turno noturno e folga 36 horas consecutivas.'},
                    {_24X48:['DN', 'F', 'F'], info:'24X48-D12H+N12H -> trabalha 24 horas consecutivas e folga 48 horas consecutivas.'},
                ],
                custom: [
                    { _24x24: ['M', 'M', 'N', 'F', 'F'], info:'24x24-M6H+M6H+N12H -> Trabalha 2 dias no turno matutino em jornada de 6 horas e mais um diurno em jornada de 12 horas, folgando assim 24 horas consecutivos'},
                    { _24x24: ['V', 'V', 'N', 'F', 'F'], info:'24x24-M6H+M6H+N12H -> Trabalha 2 dias no turno vespertino em jornada de 6 horas e mais um diurno em jornada de 12 horas, folgando assim 24 horas consecutivos'}
                ]  
           }
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
    },
    created() {
        console.log(this.cycles.custom[0]._24x24[0])
        let lengthCycle = 31;
        let rp = lengthCycle / this.cycles.custom[0]._24x24.length;//quantas repeticoes 
        console.log('inteiro: ',parseInt(rp, 10))
        let md = lengthCycle % this.cycles.custom[0]._24x24.length;//resto para completar os 28
        console.log('resto: ', md)
        let cont = 0;
        let arr = [];
        while(cont < rp) {
            this.cycles.custom[0]._24x24.forEach( (item) => {
                arr.push(item)
            })
            cont = cont + 1;
        }
        let i = 0;
        while(md > 0) {
            arr.push(this.cycles.custom[0]._24x24[i])
            md--;
            i++;
        }
        console.log(arr)
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