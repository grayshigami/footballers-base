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
                <input type="selector" id="nationalityName" v-model="newForward.nationality.name">
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
                    <label for="tc">Team country</label>
                    <input type="text" id="tc" v-model="newForward.tc">
                </div>
            </div>
        </div>
        <button @click="visible = false">Cancel</button>
        <button @click="insertForward">Insert</button>
    </pv-dialog>
    <pv-dialog class="fb-dialog" header="Update forward" v-model:visible="updateVisible" modal>
        <div class="inside-dialog">
            <div class="two-inp">
                <label for="newName">Name</label>
                <input type="text" id="newName" v-model="updatedForward.name">
                <label for="newNationalityName">Nationality name</label>
                <input type="text" id="newNationalityName" v-model="updatedForward.nationality.name">
            </div>
            <label for="newNationalityFlag">Nationality flag</label>
            <input type="text" id="newNationalityFlag" v-model="updatedForward.nationality.flag">
            <label for="newCountryOfBirthFlag">Country of birth flag</label>
            <input type="text" id="newCountryOfBirthFlag" v-model="updatedForward.countryOfBirth.flag">
            <div class="divider">
                <div class="left">
                    <label for="newBirthplace">Birthplace</label>
                    <input type="text" id="newBirthplace" v-model="updatedForward.birthplace">
                    <label for="newCountryOfBirth">Country of birth</label>
                    <input type="text" id="newCountryOfBirth" v-model="updatedForward.countryOfBirth.name">
                    <label for="newPosition">Position</label>
                    <input type="text" id="newPosition" v-model="updatedForward.position">
                    <label for="newHeight">Height</label>
                    <input type="number" id="newHeight" v-model="updatedForward.height">
                    <label for="newBirthday">Birthday</label>
                    <input type="text" id="newBirthday" v-model="updatedForward.birthday">
                    <label for="newCaps">Caps</label>
                    <input type="number" id="newCaps" v-model="updatedForward.caps">
                </div>
                <div class="right">
                    <label for="newGoals">Goals</label>
                    <input type="number" id="newGoals" v-model="updatedForward.goals">
                    <label for="newIntCaps">IntCaps</label>
                    <input type="number" id="newIntCaps" v-model="updatedForward.intCaps">
                    <label for="newIntGoals">IntGoals</label>
                    <input type="number" id="newIntGoals" v-model="updatedForward.intGoals">
                    <label for="newTeam">Team</label>
                    <input type="text" id="newTeam" v-model="updatedForward.team.name">
                    <label for="newTeamLogo">Team logo</label>
                    <input type="text" id="newTeamLogo" v-model="updatedForward.team.logo">
                    <label for="newtc">Team country</label>
                    <input type="text" id="newtc" v-model="updatedForward.tc">
                </div>
            </div>
        </div>
        <button @click="updateVisible = false">Cancel</button>
        <button @click="updateForward">Update</button>
    </pv-dialog>
    <table class="fw-table">
        <thead>
            <tr>
                <th>-</th>
                <th>-</th>
                <th>-</th>
                <th>-</th>
                <th>-</th>
                <th>-</th>
                <th>
                    <select name="" id="" v-model="filters.heightComparing">
                        <option value="equal" selected>Equal</option>
                        <option value="greater">Greater</option>
                        <option value="lower">Lower</option>
                    </select>
                </th>
                <th>-</th>
                <th>
                    <select name="" id="" v-model="filters.capsComparing">
                        <option value="equal">Equal</option>
                        <option value="greater">Greater</option>
                        <option value="lower">Lower</option>
                    </select>
                </th>
                <th>
                    <select name="" id="" v-model="filters.goalsComparing">
                        <option value="equal">Equal</option>
                        <option value="greater">Greater</option>
                        <option value="lower">Lower</option>
                    </select>
                </th>
                <th>
                    <select name="" id="" v-model="filters.intCapsComparing">
                        <option value="equal">Equal</option>
                        <option value="greater">Greater</option>
                        <option value="lower">Lower</option>
                    </select>
                </th>
                <th>
                    <select name="" id="" v-model="filters.intGoalsComparing">
                        <option value="equal">Equal</option>
                        <option value="greater">Greater</option>
                        <option value="lower">Lower</option>
                    </select>
                </th>
                <th>-</th>
                <th>-</th>
                <th>-</th>
            </tr>
            <tr>
                <th>*</th>
                <th>
                    <input type="text" v-model="filters.name">
                </th>
                <th>
                    <input type="text" v-model="filters.nationality.name">
                </th>
                <th>
                    <input type="text" v-model="filters.birthplace">
                </th>
                <th>
                    <input type="text" v-model="filters.countryOfBirth.name">
                </th>
                <th>
                    <input type="text" v-model="filters.position">
                </th>
                <th>
                    <input type="text" class="gci" v-model="filters.height">
                </th>
                <th>
                    <input type="text" class="igci" v-model="filters.birthday">
                </th>
                <th>
                    <input type="text" class="gci" v-model="filters.caps">
                </th>
                <th>
                    <input type="text" class="gci" v-model="filters.goals">
                </th>
                <th>
                    <input type="text" class="igci" v-model="filters.intCaps">
                </th>
                <th>
                    <input type="text" class="igci" v-model="filters.intGoals">
                </th>
                <th>
                    <input type="text" v-model="filters.team.name">
                </th>
                <th>
                    <input type="text" class="it" v-model="filters.tc">
                </th>
                <th>*</th>
            </tr>
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
                <th @click="sortByColumn('tc')">
                    TC
                    <i v-if="sortBy === 'tc' && sortDirection === 'asc'" class="fa-solid fa-sort-up"></i>
                    <i v-else-if="sortBy === 'tc' && sortDirection === 'desc'" 
                    class="fa-solid fa-sort-down"></i>
                    <i v-else class="fa-solid fa-sort header-icon"></i>
                </th>
                <th>*</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="forward in filteredForwards" :key="forward.id">
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
                <td>{{ forward.tc }}</td>
                <td>
                    <i class="fa-solid fa-pen-to-square edit-button" @click="showEditDialog(forward)"></i>
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
            forward: {},
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
                tc: ''
            },
            updatedForward: {
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
                tc: ''
            },
            filters: {
                name: '',
                nationality: {
                    name: ''
                },
                birthplace: '',
                countryOfBirth: {
                    name: ''
                },
                position: '',
                height: null,
                birthday: '',
                caps: null,
                goals: null,
                intCaps: null,
                intGoals: null,
                team: {
                    name: ''
                },
                tc: '',
                heightComparing: 'equal',
                capsComparing: 'equal',
                goalsComparing: 'equal',
                intCapsComparing: 'equal',
                intGoalsComparing: 'equal'
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
    computed: {
        filteredForwards() {
            return this.forwards.filter(forward => {
                const filterName = this.filters.name.toLowerCase();
                const filterNationality = this.filters.nationality.name.toLowerCase();
                const filterBirthplace = this.filters.birthplace.toLowerCase();
                const filterCountryOfBirth = this.filters.countryOfBirth.name.toLowerCase();
                const filterPosition = this.filters.position.toLowerCase();
                const filterHeight = this.filters.height;
                const filterBirthday = this.filters.birthday.toLowerCase();
                const filterCaps = this.filters.caps;
                const filterGoals = this.filters.goals;
                const filterIntCaps = this.filters.intCaps;
                const filterIntGoals = this.filters.intGoals;
                const filterTeam = this.filters.team.name.toLowerCase();
                const filterTc = this.filters.tc.toLowerCase();
                const heightComparing = this.filters.heightComparing;
                const capsComparing = this.filters.capsComparing;
                const goalsComparing = this.filters.goalsComparing;
                const intCapsComparing = this.filters.intCapsComparing;
                const intGoalsComparing = this.filters.intGoalsComparing;

                const matchesFilterName = !filterName || forward.name.toLowerCase().includes(filterName);
                const matchesFilterNationality = !filterNationality || forward.nationality.name.toLowerCase()
                .includes(filterNationality);
                const matchesFilterBirthplace = !filterBirthplace || forward.birthplace.toLowerCase()
                .includes(filterBirthplace);
                const matchesFilterCountryOfBirth = !filterCountryOfBirth || forward.countryOfBirth.name.toLowerCase()
                .includes(filterCountryOfBirth);
                const matchesFilterPosition = !filterPosition || forward.position.toLowerCase().includes(filterPosition);
                const matchesFilterBirthday = !filterBirthday || forward.birthday.toLowerCase().includes(filterBirthday);
                const matchesFilterTeam = !filterTeam || forward.team.name.toLowerCase().includes(filterTeam);
                const matchesFilterTc = !filterTc || forward.tc.toLowerCase().includes(filterTc);

                
                let matchesFilterHeight = true;
                let matchesFilterCaps = true;
                let matchesFilterGoals = true;
                let matchesFilterIntCaps = true;
                let matchesFilterIntGoals = true;

                if (filterHeight) {
                    const height = parseFloat(filterHeight);

                    if (heightComparing === 'greater') {
                        matchesFilterHeight = forward.height > height;
                    } else if (heightComparing === 'lower') {
                        matchesFilterHeight = forward.height < height;
                    } else if (heightComparing === 'equal') {
                        matchesFilterHeight = forward.height === height;
                    }
                }

                if (filterCaps) {
                    const caps = parseInt(filterCaps);

                    if (capsComparing === 'greater') {
                        matchesFilterCaps = forward.caps > caps;
                    } else if (capsComparing === 'lower') {
                        matchesFilterCaps = forward.caps < caps;
                    } else if (capsComparing === 'equal') {
                        matchesFilterCaps = forward.caps === caps;
                    }
                }

                if (filterGoals) {
                    const goals = parseInt(filterGoals);

                    if (goalsComparing === 'greater') {
                        matchesFilterGoals = forward.goals > goals;
                    } else if (goalsComparing === 'lower') {
                        matchesFilterGoals = forward.goals < goals;
                    } else if (goalsComparing === 'equal') {
                        matchesFilterGoals = forward.goals === goals;
                    }
                }

                if (filterIntCaps) {
                    const intCaps = parseInt(filterIntCaps);

                    if (intCapsComparing === 'greater') {
                        matchesFilterIntCaps = forward.intCaps > intCaps;
                    } else if (intCapsComparing === 'lower') {
                        matchesFilterIntCaps = forward.intCaps < intCaps;
                    } else if (intCapsComparing === 'equal') {
                        matchesFilterIntCaps = forward.intCaps === intCaps;
                    }
                }

                if (filterIntGoals) {
                    const intGoals = parseInt(filterIntGoals);

                    if (intGoalsComparing === 'greater') {
                        matchesFilterIntGoals = forward.intGoals > intGoals;
                    } else if (intGoalsComparing === 'lower') {
                        matchesFilterIntGoals = forward.intGoals < intGoals;
                    } else if (intGoalsComparing === 'equal') {
                        matchesFilterIntGoals = forward.intGoals === intGoals;
                    }
                }

                return matchesFilterName && matchesFilterNationality && matchesFilterBirthplace &&
                matchesFilterCountryOfBirth && matchesFilterPosition && matchesFilterHeight && matchesFilterBirthday &&
                matchesFilterCaps && matchesFilterGoals && matchesFilterIntCaps && matchesFilterIntGoals &&
                matchesFilterTeam && matchesFilterTc;
            });
        },
    },
    methods: {
        async insertForward() {
            this.visible = false;
            try {
                await axios.post('http://localhost:3000/api/v1/forwards', this.newForward);
                this.getForwards();
                this.newForward = {
                    newName: '',
                    newNationality: {
                        flag: '',
                        name: ''
                    },
                    newBirthplace: '',
                    newCountryOfBirth: {
                        flag: '',
                        name: ''
                    },
                    newPosition: '',
                    newHeight: 0.00,
                    newBirthday: '',
                    newCaps: 0,
                    newGoals: 0,
                    newIntCaps: 0,
                    newIntGoals: 0,
                    newTeam: {
                        logo: '',
                        name: ''
                    },
                    newTc: ''
                };
            } catch (error) {
                console.error('Error inserting forward:', error);
            }
        },
        showEditDialog(forward) {
            this.forward = { ...forward };
            this.updatedForward.name = forward.name;
            this.updatedForward.nationality.flag = forward.nationality.flag;
            this.updatedForward.nationality.name = forward.nationality.name;
            this.updatedForward.birthplace = forward.birthplace;
            this.updatedForward.countryOfBirth.flag = forward.countryOfBirth.flag;
            this.updatedForward.countryOfBirth.name = forward.countryOfBirth.name;
            this.updatedForward.position = forward.position;
            this.updatedForward.height = forward.height;
            this.updatedForward.birthday = forward.birthday;
            this.updatedForward.caps = forward.caps;
            this.updatedForward.goals = forward.goals;
            this.updatedForward.intCaps = forward.intCaps;
            this.updatedForward.intGoals = forward.intGoals;
            this.updatedForward.team.logo = forward.team.logo;
            this.updatedForward.team.name = forward.team.name;
            this.updatedForward.tc = forward.tc;
            this.updateVisible = true;
        },
        async updateForward() {
            this.updateVisible = false;
            try {
                const response = await axios.put(`http://localhost:3000/api/v1/forwards/${this.forward.id}`, {
                    ...this.forward,
                    name: this.updatedForward.name,
                    nationality: {
                        flag: this.updatedForward.nationality.flag,
                        name: this.updatedForward.nationality.name
                    },
                    birthplace: this.updatedForward.birthplace,
                    countryOfBirth: {
                        flag: this.updatedForward.countryOfBirth.flag,
                        name: this.updatedForward.countryOfBirth.name
                    },
                    position: this.updatedForward.position,
                    height: this.updatedForward.height,
                    birthday: this.updatedForward.birthday,
                    caps: this.updatedForward.caps,
                    goals: this.updatedForward.goals,
                    intCaps: this.updatedForward.intCaps,
                    intGoals: this.updatedForward.intGoals,
                    team: {
                        logo: this.updatedForward.team.logo,
                        name: this.updatedForward.team.name
                    },
                    tc: this.updatedForward.tc
                });

                const index = this.forwards.findIndex(f => f.id === this.forward.id);

                if (index !== -1) {
                    this.forwards.splice(index, 1, response.data);
                }

                this.forwards = [...this.forwards];
            } catch (error) {
                console.error('Error saving changes:', error);
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
        applyFilters() {},
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
    margin-top: 20px;
    box-sizing: border-box;
    padding-left: 5px;
    padding-right: 5px;
    width: 100%;
}

th input {
    box-sizing: border-box;
    width: 100%;
    padding: 4px;
}

.gci {
    width: 60px;
}

.igci {
    width: 70px;
}

.it {
    width: 50px;
}

.fw-table td, th {
    text-align: left;
}

th:hover {
    cursor: pointer;
}

th {
    font-size: 14px;
    padding: 5px;
}

td {
    font-size: 14px;
    border-top: 1px solid black;
    padding: 4px;
}

.selector {
    width: 15px;
    height: 15px;
}

.edit-button:hover {
    cursor: pointer;
}
</style>