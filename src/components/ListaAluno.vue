<template>
	<section class="lista">
		<ul>
			<li v-for="studant in ordenedStudents">
				<strong>{{studant.name}}</strong><br>
				<span>{{studant.age}} anos.</span>			
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
		}
	}
</script>
<style>
	.lista{
		background-color: green;
		display: flex;
		width: 250px;
		margin:30px;
		padding: 10px;
		align-content: flex-end;
		color: white;
		justify-content: flex-start;
		list-style: none;
	}
</style>