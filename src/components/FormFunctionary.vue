<template>
    <div class="row form-employee">
        <div class="col-sm-4">
            <label for="Escala">Escala</label>
            <select class="form-control" v-model.number="cycle">
                <option selected value="0">Escolha o tipo de cilclo</option>
                <option value="1">Ciclo V-V-N-F-F (V-Vespertino -> Das 13:00 às 19:00, N-Noturno -> Das 19:00 às 07:00, F-Folga)</option>
                <option value="2">Ciclo M-M-N-F-F (M-Matutino -> Das 07:00 às 13:00, N-Noturno -> Das 19:00 às 07:00, F-Folga)</option>
                <option value="3">Ciclo M-M-M-M-M-M-F ((M-Matutino -> Das 07:00 às 13:00, F-Folga Somente aos Domingos)</option>
                <option value="4">Ciclo D-D-D-D-D-F-F (D-Diurno -> Das 08:00 às 17:00, Horário comercial, F-Folga aos Finais de Semana)</option>
            </select>
        </div>
        <div class="col-sm-2">
            <label for="Register">Matrícula:</label>
            <input type="number" class="form-control form-matricula" placeholder="Digite a matrícula" v-model.number="register">
        </div>
        <div class="col-sm-4">
            <label for="Name">Funcionário:</label>
            <input type="text"  class="form-control form-name" placeholder="Digite o nome do funcionário" v-model="name"> {{name}}
        </div>
        <div class="col-sm-1 btn btn-primary btn-small" @click="addFuncionrio">Adicionar</div>
    </div>
</template>

<script>
// import barramento from '../barramento/barramento.js';

export default {
    data() {
        return {
            register: '',
            name: '',
            cycle: '0'
        }
    },
    methods: {
        addFuncionrio() {
            const functionary = {
                id: this.register,
                register: this.register,
                name: this.name,
                cycle: this.cycle
            }
            this.register = ''
            this.name = ''
            this.cycle = ''
            this.$store.state.functionaries.push(functionary)
            //eslint-disble-next-line
            console.log('chamado', functionary)
        }
    }
}
</script>

<style>
/* div.form-employee {
    width: 400px;
}     */
div.btn-small {
    margin-top: 27px;
    width: 100px;
    height: 38px;
    margin-left: 20px;
}
</style>