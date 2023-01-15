<template>
    <div>
        <h2>Daily Notes</h2>
        <form v-on:submit.prevent="addNote">
            <div class="form-group">
                <label for="highlight">Highlight</label>
                <input type="text" v-model="highlight" class="form-control form-control-sm" name="highlight" required>
            </div>
            <div class="form-group">
                <label for="grateful">Grateful</label> 
                <input type="text" v-model="grateful" class="form-control form-control-sm" name="grateful" required>
            </div>
            <div class="form-group">
                <label for="letgo">Let Go</label>
                <input type="text" v-model="letgo"  class="form-control form-control-sm" name="letgo" required>
            </div>
            <button type="submit" class="btn btn-primary">Add</button>
        </form>
        <div class="d-flex overflow-scroll">
            <div v-for="note in notes" v-bind:key="note.id" class="border rounded mt-2 p-4 mr-1 col">
                <h5>{{ note.date }}</h5>
                <p>Highlight: {{ note.highlight }}</p>
                <p>Grateful: {{ note.grateful }}</p>
                <p>Let Go: {{ note.letgo }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "DayNotes",
    data() {
        return {
            notes: [],
            date: new Date().toJSON().slice(0,10).replace(/-/g,'/'),
            highlight: '',
            grateful: '',
            letgo: '',
        }
    },
    methods: {
        addNote() {
            let noteEntry = {
                id: this.notes.length,
                date: this.date,
                highlight: this.highlight,
                grateful: this.grateful,
                letgo: this.letgo
            }
            this.notes = [...this.notes, noteEntry]
            localStorage.setItem('notes', JSON.stringify(this.notes))
        }
    },
    mounted() {
        const existingNotes = localStorage.getItem('notes')
        this.notes = JSON.parse(existingNotes)||[]
    }
}
</script>