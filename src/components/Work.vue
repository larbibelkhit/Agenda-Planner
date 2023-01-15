<template>
    <div>
        <h2>Work</h2>
        <form v-on:submit.prevent="addWorkTask">
            <div class="form-row">
                <div class="form-group col">
                    <label for="text">Text</label> 
                    <input required type="text" v-model="taskText" name="text" class="form-control form-control-sm">
                </div>
                <div class="form-group col">
                    <label for="team">Team</label>
                    <select required v-model="taskTeam" name="team" class="form-control form-control-sm">
                        <option value="" disabled>Team</option>
                        <option value="AI">AI</option>
                        <option value="Atlas">Atlas</option>
                        <option value="Networks">Networks</option>
                        <option value="Consumer Technology">Consumer Technology</option>
                    </select>
                </div>
            </div>
            <div class="form-group">
                <label for="deadline">Deadline</label> 
                <input type="date" v-model="taskDeadline" class="form-control form-control-sm" name="deadline">
            </div>
            <button class="btn btn-primary">Add</button>
        </form>
        <div v-if="workTasks.length > 0" class="mt-3">
            <table class="table">
                <thead class="thead-light">
                    <tr>
                        <th>Task</th>
                        <th>Team</th>
                        <th>Deadline</th>
                        <th>Complete</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="task in workTasks" v-bind:key="task.id">
                        <td>{{ task.text }}</td>
                        <td>{{ task.team }}</td>
                        <td>{{ task.deadline }}</td>
                        <td>
                            <input type="checkbox" @change="updateWorkTask(task.id)" :checked="task.complete">
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div v-else class="mt-3">No Work Tasks at the moment</div>
    </div>
</template>

<script>
export default {
    name: "Work",
    data() {
        return {
            workTasks: [],
            taskText: '',
            taskTeam: null,
            taskDeadline: new Date().toJSON().slice(0,10)
        }
    },
    methods: {
        addWorkTask() {
            let workTaskEntry = {
                id: this.workTasks.length,
                text: this.taskText,
                team: this.taskTeam,
                deadline: this.taskDeadline,
                complete: false
            }
            this.workTasks = [...this.workTasks, workTaskEntry]
            localStorage.setItem('work tasks', JSON.stringify(this.workTasks))
        },
        updateWorkTask(id) {
            this.workTasks[id].complete = !this.workTasks[id].complete
            localStorage.setItem('work tasks', JSON.stringify(this.workTasks))
        }
    },
    mounted(){
        const existingWorkTasks = localStorage.getItem('work tasks')
        this.workTasks = JSON.parse(existingWorkTasks) || []
    }
}
</script>