<template>
	<div class="main">
			<section class="campo">
				<label>Nome</label>
				<input v-model="name" type="text">
				<br>
				<label>Idade</label>
				<input v-model="age" type="text">
				<br>
				<button @click="enviar">Enviar</button>
			</section>
			<section class="selecao">
				<label>Ordenar por:</label>
				<select v-model="configs.orderBy">
					<option value="name">nome</option>
					<option value="age">Idade</option>
				</select>
				<br>
				<label>Ordem</label>
				<select v-model="configs.order">
					<option value="asc">Crescente</option>
					<option value="desc">Decrescente</option>
				</select>
					<br>
					<label>Filtro</label>
					<input type="text" v-model="configs.filter" placeholder="Filtrar por nome">
			</section>
		<ListaAluno
			v-bind:ordenedStudents="ordenedStudents"
			@removeAluno="value => {removeAluno = value}"
			@remove="value => {remove = value}"
		></ListaAluno>
	</div>
</template>
<script>
import _ from 'lodash'
import ListaAluno from './ListaAluno.vue'
export default{
	name:'CadastroAluno',
	data(){
		return{
			name:'',
			age:'',
			remove:false,
			removeAluno:'',
			configs:{
				orderBy:'name',
				order:'asc',//desc
				filter:''
			},
			studants:[
				{
					name:'Renan',
					age:'33'
				},
				{
					name:'Caio',
					age:'16' 
				},
				{
					name:'Rômulo',
					age:'30'

				},
				{
					name:'Anna',
					age:'25'
				}
			]

		}
	},
	watch:{
		removeAluno(){
			if (this.remove === true) {
				this.studants.splice(this.removeAluno,1)
				this.remove = false
				this.removeAluno = ''
			}	
		}

	},
	computed:{
		ordenedStudents(){
			const filter = this.configs.filter
			const studants = _.orderBy(this.studants, this.configs.orderBy, this.configs.order)
			if(_.isEmpty(filter)){
				return studants
			}
			return _.filter(studants, studant => studant.name.indexOf(filter) >=0)
		}
	},
	methods:{
		enviar(){
			this.studants.push({
				name: this.name,
				age: this.age
			})
			this.name = ''
			this.age = ''
		}
	},
	components:{
		ListaAluno
	}
}
</script>
<style>
*{
	margin:0px;
	padding: 0px;
}
	li strong{
		font-size: 20px;
	}
	.main{
		max-width: 620px;
		max-height: 520px;
		border-color: #6dccab;
		border:40px;
		background: #6dccab;
		background-size: cover;
		display: flex;
		flex-direction: row;
	}
	/*.esquerda{
		display: flex;
		flex-direction: wrap;
	}*/
	.lista{
		background-color: green;
		display: flex;
		max-width: 300vh;
		max-height: 520px;
		margin:0px;
		padding: 0px;
		align-content: flex-end;
		color: white;
		justify-content: flex-start;
		list-style: none;
	}
	.campo{
		display: flex;
		background-color: orange;
		max-width: 50%;
		max-height: 360px;
		margin: 10px;
		padding: 5px;
		align-items: center;
		flex-direction: column;
		
	}
	.selecao{
		display: flex;
		background-color: purple;
		max-width: 50%;
		max-height: 360px;
		margin: 10px;
		padding: 5px;
		color: white;
		align-items: center;
		flex-direction: column;

	}
</style>