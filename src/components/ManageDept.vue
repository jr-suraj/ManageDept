<template>

	<v-container>
		
	<v-card
		class="mx-auto"
	>
		<form @submit.prevent="addDept()">
			<v-text-field
				v-model="newdept"
				label="New Department"
				prepend-inner-icon="mdi-plus-thick"
				filled
				required
			></v-text-field>
		</form>
		<v-col>
			<v-row>
				
				<v-col cols="12 py-0">
					<v-expansion-panels 
						v-model="panel"
						>
						<v-expansion-panel>
						<v-expansion-panel-header>MAIN DEPARTMENTS</v-expansion-panel-header>
						<v-expansion-panel-content class="pt-4">
							<ul class="dept-list">
								<li class="text-capitalize" v-for="(department, index) in departments" :key="index">
									{{ department.name }}
									<v-btn @click="removeDept(index)" class="ml-auto" text icon color="red">
									<v-icon>mdi-close-circle</v-icon>
									</v-btn>
								</li>
							</ul>
						</v-expansion-panel-content>
						</v-expansion-panel>
					</v-expansion-panels>
				</v-col>
			</v-row>			
		</v-col>

		<v-tabs
			v-model="currentDepartment"
			center-active
			background-color="teal darken-1"
			dark
			next-icon="mdi-arrow-right-bold-box-outline"
			prev-icon="mdi-arrow-left-bold-box-outline"
			show-arrows
		>
		<v-tabs-slider></v-tabs-slider>
			<v-tab
			v-for="(data, index) in departments"
			:key="index"
			>
			{{ data.name }}
			</v-tab>
			<v-tab-item v-for="dpt in departments" :key="dpt.id">
				<b-card-group deck>
					<b-card>
						<form @submit.prevent="addSub(dpt)">
							<v-text-field
								v-model="newsub"
								label="New sub-department"
								prepend-inner-icon="mdi-plus-thick"
								filled
								required
							></v-text-field>
						</form>
						
						<b-list-group>
							<draggable v-model="dpt.subs" draggable=".subs" @start="drag=true" @end="drag=false">
								<transition-group type="transition" name="flip-list">
									<b-list-group-item class="subs d-flex align-items-center" v-for="(data, index) in dpt.subs" :key="data.id">{{data.name}} 
										<v-btn @click="removeSub(dpt, index)" class="ml-auto" outlined fab x-small color="red">
										<v-icon>mdi-trash-can-outline</v-icon>
										</v-btn>
									</b-list-group-item>
								</transition-group>
							</draggable>
						</b-list-group>
					</b-card>
				</b-card-group>
			</v-tab-item>
		</v-tabs>
		
	</v-card>
</v-container>
</template>

<script>
import draggable from 'vuedraggable';
export default {
	components: {
		draggable,
	},
	data: () => ({
		panel: 0,
		newdept: '',
		newsub: '',
		currentDepartment: null,
		departments : [
			{
				"id": 1,
				"name": "Office",
				"subs": [
					{id:1, name: "Account Team"},
					{id:2, name: "Finance Team"},
					{id:3, name: "Admin Team"},
				],
			},
			{
				"id": 2,
				"name": "Information Technology",
				"subs": [
					{id:1, name: "iOS Team"},
					{id:2, name: "Android Team"},
					{id:3, name: "Web Team"},
					{id:4, name: ".Net Team"},
					{id:5, name: "Java Team"},
				],
			},
			{
				"id": 3,
				"name": "Transportation",
				"subs": [
					{id:1, name: "Driver Team"},
					{id:2, name: "Mechanic Team"},
					{id:3, name: "Logistic Team"},
				],
			},
			{
				"id": 4,
				"name": "Logistic",
				"subs": [
					{id:1, name: "Driver Team"},
					{id:2, name: "Mechanic Team"},
					{id:3, name: "Logistic Team"},
				],
			},
		],
		
	}),
	methods: {
		//Adding New Main Department
		addDept(){
			this.departments.push({
				id: this.departments.length + 1,
				name:this.newdept,
				subs: [],
			});
			this.newdept = '';
		},
		//Removing Main Department
		removeDept (index) {
			if(confirm("Do you really want to delete?")){
				this.departments.splice(index, 1);
			}
		},
		//Adding New Sub Departments
		addSub(dpt){
			dpt.subs.push({
				id: dpt.subs.length + 1,
				name:this.newsub
			});
			this.newsub = '';
		},
		//Removing Sub Departments
		removeSub (dpt, index) {
			if(confirm("Do you really want to delete?")){
				dpt.subs.splice(index, 1);
			}
		},
	},
}
</script>

<style lang="scss" scoped>
.subs {
	cursor: move;
}
.flip-list-move {
	transition: transform 0.5s; 
}
.card {
	border-radius: 0;
}
.v-tabs {
	border-top: 1px solid #ddd !important;
}
.v-messages,.v-text-field__details,.v-text-field.v-text-field--enclosed .v-text-field__details {
	min-height: 0 !important;
	margin: 0 !important;
}
.dept-list {
	list-style-type: none;
	margin: 0;
	padding: 0;
}
.dept-list li {
	display: inline-block;
	padding: 0 .5rem;
	border-radius: 25px;
	margin: .3rem;
	-webkit-box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.20);
	-moz-box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.20);
	box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.20);
}
</style>