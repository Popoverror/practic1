<script>
export default {
	data() {
		return {
			age: 0,
			messageLazy: "",
			messageTrim: "",
			searchTerm: '',
			addStudentsState: {
				id: '1',
				fullName: '',
				group: 'A',
				yearOfBirth: '',
				passed: false
			},
			num1: 100,
			num2: 200,
			total: '',
			styleobj: {
				width: '100px',
				height: '100px',
				backgroundColor: 'red'
			},
			students: [
				{
					id: 0,
					fullName: 'John Smith',
					group: 'A',
					yearOfBirth: 2000,
					passed: true
				},
				{
					id: 1,
					fullName: 'Zack Philips',
					group: 'B',
					yearOfBirth: 2001,
					passed: false
				},
				{
					id: 2,
					fullName: 'Jack Johnson',
					group: 'C',
					yearOfBirth: 2002,
					passed: true
				}
			]
		}
	},
	methods: {
		checkStudentOnSearch(fullName) {
			if (this.searchTerm === '') return

			const loweredFullName = fullName.toLowerCase()
			const loweredSearchTerm = this.searchTerm.toLowerCase()

			return loweredFullName.indexOf(loweredSearchTerm) >= 0
		},
		deleteStudent(id) {
			const index = this.students.findIndex(student => student.id === id)
			this.students.splice(index, 1)
		},
		addStudent() {
			this.students.push(JSON.parse(JSON.stringify(this.addStudentsState)))
			this.addStudentsState.id = this.students.length + 1
			this.addStudentsState.fullName = 'j'
			this.addStudentsState.group = 'A'
			this.addStudentsState.yearOfBirth = '2022'
			this.addStudentsState.passed = false
		},
		changebgcolor: function () {
			this.styleobj.backgroundColor = 'green'
		},
		originalcolor: function () {
			this.styleobj.backgroundColor = 'red'
		}
	}
}
</script>

<template>
	<div class="addStudent test" @submit.prevent="addStudent">
		<label class="addStudentLabel">
			Name
			<input type="text" v-model="addStudentsState.fullName" />
		</label>

		<label class="addStudentLabel">
			Gruppe
			<select class="select" v-model="addStudentsState.group">
				<option value="A">A</option>
				<option value="B">B</option>
				<option value="C">C</option>
			</select>
		</label>

		<label class="addStudentLabel">
			Geburtstagdatum
			<input type="dateOfBirthday" v-model="addStudentsState.yearOfBirth" />
		</label>

		<label class="addStudentLabel">
			passt
			<input v-model="addStudentsState.passed" type="checkbox" />
		</label>

		<button class="addStudentButton" @click="addStudent()">
			hinzuf??gen
		</button>
		<br />
		<br />
		<hr />
		<br />
	</div>
	<div class="test">
		<label>
			Search:
			<input type="text" v-model="searchTerm" />
		</label>

		<table>
			<tr>
				<th>Name</th>
				<th>Gruppe</th>
				<th>Geburtstagdatum</th>
				<th>Hat die Arbeit gemacht</th>
				<th>L??schen Schaltfl??che</th>
			</tr>

			<tr v-for="student in students" :key="student.id"
				:class="checkStudentOnSearch(student.fullName) && 'studentHighlight'">
				<td>{{ student.fullName }}</td>
				<td>{{ student.group }}</td>
				<td>{{ student.yearOfBirth }}</td>
				<td>
					<input type="checkbox" v-model="student.passed" />
				</td>
				<td>
					<button v-on:click="deleteStudent(student.id)">L??schen</button>
				</td>
			</tr>
		</table>
	</div>
	<br />
	<hr />
	<br />
	<div class="test">
		<h3>Task 1</h3>
		<span style="font-size: 25px">EnterAge: {{ age }}</span>
		<input v-model.number="age" type="number" />
		<br />
		<span style="font-size: 25px">EnterMessage: {{ messageLazy }}</span>
		<input v-model.lazy="messageLazy" />
		<br />
		<span style="font-size: 25px">EnterMessage : {{ messageTrim }}</span>
		<input v-model.trim="messageTrim" />
	</div>
	<div id="databinding" class="test">
		<br />
		<hr />
		<br />
		<h3>Task 2</h3>
		<div v-bind:style="styleobj" v-on:mouseover="changebgcolor" v-on:mouseout="originalcolor"></div>
	</div>
</template>

<style scoped>
header {
	line-height: 1.5;
}

.test {
	justify-content: center;
	flex-direction: column;
	align-items: flex-start;
}

.logo {
	display: block;
	margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
	header {
		display: flex;
		place-items: center;
		padding-right: calc(var(--section-gap) / 2);
	}

	.logo {
		margin: 0 2rem 0 0;
	}

	header .wrapper {
		margin: 0, auto;
	}
}

.studentHighlight {
	color: rgb(102, 217, 243);
}
</style>
