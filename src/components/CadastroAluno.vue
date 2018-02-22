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
		<ListaAluno v-bind:ordenedStudents="ordenedStudents"></ListaAluno>
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
		background: #00f url(https://i3.wp.com/www.zastavki.com/pictures/originals/2012/Backgrounds_Water_drops_035501_.jpg)no-repeat fixed ;
		background-size: cover;
		display: flex;
		flex-wrap: wrap;
	}
	.campo{
		display: flex;
		background-color: orange;
		width: 250px;
		margin:30px;
		padding: 10px;
		align-items: center;
		flex-direction: column;
		
	}
	.selecao{
		display: flex;
		background-color: purple;
		width: 250px;
		margin:30px;
		padding: 10px;
		color: white;
		align-items: center;
		flex-direction: column;

	}
</style>