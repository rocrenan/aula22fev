<template>
	<section class="lista">
		<ul>
			<li v-for="(studant, index) in ordenedStudents">
				<strong>{{studant.name}}</strong><br>
				<span>{{studant.age}} anos.</span>
				<button @click="removeAluno(index)"> X </button>		
			</li>
		</ul>
	</section>
</template>
<script>
export default{
	name:'',
	props:{
		ordenedStudents:{
			type:Array,
			required:true
		}
	},
	data(){
		return{

		}
	},
	methods:{
		removeAluno(value){
			this.$emit('remove',true)
			this.$emit('removeAluno', value)
		}
	}	
}
</script>
<style>
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
</style>