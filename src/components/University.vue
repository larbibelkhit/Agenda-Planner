<template>
    <div>
        <h2>University</h2>
        <form v-on:submit.prevent="addUniTask">
            <div class="form-row">
                <div class="form-group col">
                    <label for="task">Task</label>
                    <input required type="text" v-model="taskText" class="form-control form-control-sm" name="task">
                </div>
                <div class="form-group col">
                    <label for="type">Type</label> 
                    <select required v-model="taskType" class="form-control form-control-sm" name="type">
                        <option value="" disabled>Task Type</option>
                        <option value="Exam">Exam</option>
                        <option value="Coursework">Coursework</option>
                        <option value="Lab Session">Lab Session</option>
                        <option value="Exercise">Exercise</option>
                    </select>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group col">
                    <label for="module">Module</label> 
                    <select required v-model="taskModule" class="form-control form-control-sm">
                        <option value="" disabled>Task Module</option>
                        <option value="Security Engineering">Security Engineering</option>
                        <option value="User Experience Design">User Experience Design</option>
                        <option value="Neural Networks">Neural Networks</option>
                        <option value="Final Year Project">Final Year Project</option>
                    </select>
                </div>
                <div class="form-group col">
                    <label for="deadline">Deadline</label>
                    <input type="date" v-model="taskDeadline" name="deadline" class="form-control form-control-sm">
                </div>
            </div>
            <button class="btn btn-primary">Add</button>
        </form>
        <div v-if="uniTasks.length > 0" class="mt-3">
            <table class="table">
                <thead class="thead-light">
                    <tr>
                        <th>Task</th>
                        <th>Type</th>
                        <th>Module</th>
                        <th>Deadline</th>
                        <th>Complete</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="task in uniTasks" v-bind:key="task.id">
                        <td>{{ task.text }}</td>
                        <td>{{ task.type }}</td>
                        <td>{{ task.module }}</td>
                        <td>{{ task.deadline }}</td>
                        <td>
                            <input type="checkbox" @change="updateUniTask(task.id)" :checked="task.complete">
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div v-else class="mt-3">No Uni Tasks at the moment</div>
    </div>
</template>

<script>
export default {
    name: "University",
    data() {
        return {
            uniTasks: [],
            taskText: '',
            taskType: null,
            taskModule: null,
            taskDeadline: new Date().toJSON().slice(0,10),
        }
    },
    methods: {
        addUniTask() {
            let uniTaskEntry = {
                id: this.uniTasks.length,
                text: this.taskText,
                type: this.taskType,
                module: this.taskModule,
                deadline: this.taskDeadline,
                complete: false,
            }
            this.uniTasks = [...this.uniTasks, uniTaskEntry]
            localStorage.setItem('university tasks', JSON.stringify(this.uniTasks))
        },
        updateUniTask(id) {
            this.uniTasks[id].complete = !this.uniTasks[id].complete
            localStorage.setItem('university tasks', JSON.stringify(this.uniTasks))
        }
    },
    mounted() {
        const existingUniTasks = localStorage.getItem('university tasks')
        this.uniTasks = JSON.parse(existingUniTasks) || []
    }
}
</script>