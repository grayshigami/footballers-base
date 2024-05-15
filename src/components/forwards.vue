<template>
    <h2>Forwards</h2>
    <button class="new-button" @click="visible = true">
        <i class="fa-solid fa-plus"></i>
        Create
    </button>
    <button class="delete-button" @click="deleteSelectedForwards">
        <i class="fa-solid fa-trash"></i>
        Delete
    </button>
    <pv-dialog class="fb-dialog" header="Insert forward" v-model:visible="visible" modal>
        <div class="inside-dialog">
            <div class="two-inp">
                <label for="name">Name</label>
                <input type="text" id="name" v-model="newForward.name">
                <label for="nationalityName">Nationality name</label>
                <input type="text" id="nationalityName" v-model="newForward.nationality.name">
            </div>
            <label for="nationalityFlag">Nationality flag</label>
            <input type="text" id="nationalityFlag" v-model="newForward.nationality.flag">
            <label for="countryOfBirthFlag">Country of birth flag</label>
            <input type="text" id="countryOfBirthFlag" v-model="newForward.countryOfBirth.flag">
            <div class="divider">
                <div class="left">
                    <label for="birthplace">Birthplace</label>
                    <input type="text" id="birthplace" v-model="newForward.birthplace">
                    <label for="countryOfBirth">Country of birth</label>
                    <input type="text" id="countryOfBirth" v-model="newForward.countryOfBirth.name">
                    <label for="position">Position</label>
                    <input type="text" id="position" v-model="newForward.position">
                    <label for="height">Height</label>
                    <input type="number" id="height" v-model="newForward.height">
                    <label for="birthday">Birthday</label>
                    <input type="text" id="birthday" v-model="newForward.birthday">
                    <label for="caps">Caps</label>
                    <input type="number" id="caps" v-model="newForward.caps">
                </div>
                <div class="right">
                    <label for="goals">Goals</label>
                    <input type="number" id="goals" v-model="newForward.goals">
                    <label for="intCaps">IntCaps</label>
                    <input type="number" id="intCaps" v-model="newForward.intCaps">
                    <label for="intGoals">IntGoals</label>
                    <input type="number" id="intGoals" v-model="newForward.intGoals">
                    <label for="team">Team</label>
                    <input type="text" id="team" v-model="newForward.team.name">
                    <label for="teamLogo">Team logo</label>
                    <input type="text" id="teamLogo" v-model="newForward.team.logo">
                    <label for="teamCountry">TeamCountry</label>
                    <input type="text" id="teamCountry" v-model="newForward.teamCountry">
                </div>
            </div>
        </div>
        <button @click="visible = false">Cancel</button>
        <button @click="insertForward">Insert</button>
    </pv-dialog>
    <pv-dialog class="fb-dialog" header="Update forward" v-model:visible="updateVisible" modal>
        <div class="inside-dialog">
            <div class="two-inp">
                <label for="name">Name</label>
                <input type="text" id="name" v-model="newForward.name">
                <label for="nationalityName">Nationality name</label>
                <input type="text" id="nationalityName" v-model="newForward.nationality.name">
            </div>
            <label for="nationalityFlag">Nationality flag</label>
            <input type="text" id="nationalityFlag" v-model="newForward.nationality.flag">
            <label for="countryOfBirthFlag">Country of birth flag</label>
            <input type="text" id="countryOfBirthFlag" v-model="newForward.countryOfBirth.flag">
            <div class="divider">
                <div class="left">
                    <label for="birthplace">Birthplace</label>
                    <input type="text" id="birthplace" v-model="newForward.birthplace">
                    <label for="countryOfBirth">Country of birth</label>
                    <input type="text" id="countryOfBirth" v-model="newForward.countryOfBirth.name">
                    <label for="position">Position</label>
                    <input type="text" id="position" v-model="newForward.position">
                    <label for="height">Height</label>
                    <input type="number" id="height" v-model="newForward.height">
                    <label for="birthday">Birthday</label>
                    <input type="text" id="birthday" v-model="newForward.birthday">
                    <label for="caps">Caps</label>
                    <input type="number" id="caps" v-model="newForward.caps">
                </div>
                <div class="right">
                    <label for="goals">Goals</label>
                    <input type="number" id="goals" v-model="newForward.goals">
                    <label for="intCaps">IntCaps</label>
                    <input type="number" id="intCaps" v-model="newForward.intCaps">
                    <label for="intGoals">IntGoals</label>
                    <input type="number" id="intGoals" v-model="newForward.intGoals">
                    <label for="team">Team</label>
                    <input type="text" id="team" v-model="newForward.team.name">
                    <label for="teamLogo">Team logo</label>
                    <input type="text" id="teamLogo" v-model="newForward.team.logo">
                    <label for="teamCountry">TeamCountry</label>
                    <input type="text" id="teamCountry" v-model="newForward.teamCountry">
                </div>
            </div>
        </div>
        <button @click="updateVisible = false">Cancel</button>
        <button>Update</button>
    </pv-dialog>
    <table class="fw-table">
        <thead>
            <tr>
                <th>*</th>
                <th @click="sortByColumn('name')">
                    Name
                    <i v-if="sortBy === 'name' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'name' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('nationality')">
                    Nationality
                    <i v-if="sortBy === 'nationality' && sortDirection === 'asc'" 
                    class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'nationality' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('birthplace')">
                    Birthplace
                    <i v-if="sortBy === 'birthplace' && sortDirection === 'asc'" 
                    class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'birthplace' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('countryOfBirth')">
                    CountryOfBirth
                    <i v-if="sortBy === 'countryOfBirth' && sortDirection === 'asc'" 
                    class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'countryOfBirth' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('position')">
                    Position
                    <i v-if="sortBy === 'position' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'position' && sortDirection === 'desc'"
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('height')">
                    Height
                    <i v-if="sortBy === 'height' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'height' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('birthday')">
                    Birthday
                    <i v-if="sortBy === 'birthday' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'birthday' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('caps')">
                    Caps
                    <i v-if="sortBy === 'caps' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'caps' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('goals')">
                    Goals
                    <i v-if="sortBy === 'goals' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'goals' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('intCaps')">
                    IntCaps
                    <i v-if="sortBy === 'intCaps' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'intCaps' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('intGoals')">
                    IntGoals
                    <i v-if="sortBy === 'intGoals' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'intGoals' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('team')">
                    Team
                    <i v-if="sortBy === 'team' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'team' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th @click="sortByColumn('teamCountry')">
                    TeamCountry
                    <i v-if="sortBy === 'teamCountry' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'teamCountry' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th>*</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="forward in forwards" :key="forward.id">
                <td>
                    <input type="checkbox" v-model="selectedForwards" :value="forward.id" class="selector">
                </td>
                <td>{{ forward.name }}</td>
                <td>
                    <img :src="forward.nationality.flag" alt="" width="20" height="15">
                    {{ forward.nationality.name }}
                </td>
                <td>{{ forward.birthplace }}</td>
                <td>
                    <img :src="forward.countryOfBirth.flag" alt="" width="20" height="15">
                    {{ forward.countryOfBirth.name }}
                </td>
                <td>{{ forward.position }}</td>
                <td>{{ forward.height.toFixed(2) }}</td>
                <td>{{ forward.birthday }}</td>
                <td>{{ forward.caps }}</td>
                <td>{{ forward.goals }}</td>
                <td>{{ forward.intCaps }}</td>
                <td>{{ forward.intGoals }}</td>
                <td>
                    <img :src="forward.team.logo" alt="" width="19" height="20">
                    {{ forward.team.name }}
                </td>
                <td>{{ forward.teamCountry }}</td>
                <td>
                    <i class="fa-solid fa-pen-to-square edit-button" @click="updateVisible = true"></i>
                </td>
            </tr>
        </tbody>
    </table>
</template>
<script>
import axios from 'axios';

export default {
    name: 'forwards-component',
    data() {
        return {
            forwards: [],
            newForward: {
                name: '',
                nationality: {
                    flag: '',
                    name: ''
                },
                birthplace: '',
                countryOfBirth: {
                    flag: '',
                    name: ''
                },
                position: '',
                height: 0.00,
                birthday: '',
                caps: 0,
                goals: 0,
                intCaps: 0,
                intGoals: 0,
                team: {
                    logo: '',
                    name: ''
                },
                teamCountry: ''
            },
            selectedForwards: [],
            visible: false,
            updateVisible: false,
            sortBy: '',
            sortDirection: 'asc'
        };
    },
    mounted() {
        this.getForwards();
    },
    methods: {
        async insertForward() {
            this.visible = false;
            try {
                await axios.post('http://localhost:3000/forwards', this.newForward);
                this.getForwards();
                this.newForward = {
                    name: '',
                    nationality: {
                        flag: '',
                        name: ''
                    },
                    birthplace: '',
                    countryOfBirth: {
                        flag: '',
                        name: ''
                    },
                    position: '',
                    height: 0.00,
                    birthday: '',
                    caps: 0,
                    goals: 0,
                    intCaps: 0,
                    intGoals: 0,
                    team: {
                        logo: '',
                        name: ''
                    },
                    teamCountry: ''
                };
            } catch (error) {
                console.error('Error inserting forward:', error);
            }
        },
        getForwards() {
            axios.get('http://localhost:3000/api/v1/forwards')
            .then(response => {
                this.forwards = response.data;
            })
            .catch(error => {
                console.error('Error fetching forwards', error);
            });
        },
        deleteSelectedForwards() {
            this.selectedForwards.forEach(id => {
                axios.delete(`http://localhost:3000/api/v1/forwards/${id}`)
                .then(() => {
                    this.getForwards();
                })
                .catch(error => {
                    console.error('Error deleting forwards:', error);
                });
            })
        },
        sortByColumn(column) {
            if (column == this.sortBy) {
                this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
            } else {
                this.sortBy = column;
                this.sortDirection = 'asc';
            }

            if ((column == "Height" || column == "Caps" || column == "Goals" || column == "IntCaps" ||
                column == "IntGoals") && this.sortDirection == 'asc') {
                    this.forwards.sort(function(a, b) { return a - b });
            } else if ((column == "Height" || column == "Caps" || column == "Goals" || column == "IntCaps" ||
                column == "IntGoals") && this.sortDirection == 'desc') {
                    this.forwards.sort(function(a, b) { return b - a });
            } else {
                this.forwards.sort((a, b) => {
                if (this.sortDirection === 'asc') {
                    return a[column] > b[column] ? 1 : -1;
                } else {
                    return a[column] < b[column] ? 1 : -1;
                }
            });
        }
            }
    }
}
</script>
<style scoped>
h2 {
    margin: 20px;
}

.new-button {
    margin-left: 20px;
    background-color: rgb(10, 175, 10);
    color: white;
    font-weight: bold;
    border: none;
    font-size: 16px;
    padding: 15px;
    border-radius: 5px;
}

.new-button:hover {
    cursor: pointer;
    background-color: rgb(65, 213, 65);
}

.delete-button {
    margin-left: 20px;
    background-color: red;
    color: white;
    font-weight: bold;
    border: none;
    font-size: 16px;
    padding: 15px;
    border-radius: 5px;
}

.delete-button:hover {
    cursor: pointer;
    background-color: rgb(255, 118, 118);
}

.dialog-space {
    margin: 0 auto;
}

.fb-dialog {
    background-color: white;
}

.fb-dialog button {
    font-size: 16px;
    padding: 15px;
    margin: 10px;
}

.fb-dialog input {
    margin: 5px;
    padding: 5px;
}

.fb-dialog label {
    margin-left: 5px;
}

.inside-dialog {
    background-color: white;
    width: 100%;
    display: flex;
    flex-direction: column;
    padding: 20px;
}

.two-inp {
    display: flex;
    background-color: white;
}

.divider {
    display: flex;
    width: 90%;
}

.left, .right {
    display: flex;
    flex-direction: column;
}

.fw-table {
    font-family: arial, sans-serif;
    margin-left: 5px;
    margin-top: 20px;
}

.fw-table td, th {
    text-align: left;
    padding: 5px;
}

th:hover {
    cursor: pointer;
}

td {
    font-size: 14px;
    border-top: 1px solid black;
}

.selector {
    width: 15px;
    height: 15px;
}

.edit-button:hover {
    cursor: pointer;
}
</style>