<template>
    <div>
        <NavBar />
        <EditRecordModal :record="selectedRecord" />
        <DeleteRecordModal :record="selectedRecord" @onDeleted="getAll" />

        <div class="container">
            <h1>
                LIST OF RECORD
            </h1>
            
            <RecordEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-primary">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Age</th>
                        <th>Skills</th>
                        <th>Address</th>
                        <th>Designation</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="record in records" :key="record.id">
                        <td>{{record.name}}</td>
                        <td>{{record.age}}</td>
                        <td>{{record.skills}}</td>
                        <td>{{record.address}}</td>
                        <td>{{record.designation}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(record)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(record)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
           records: [],
            selectedRecord: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/records')
            .then((res)=>{
                if (res.status==200) {
                    this.records = res.data
                };
            })
        },
        onEdit(selectedRecord) {
            this.selectedRecord = selectedRecord
            this.$bvModal.show('editRecordModal')
        },
        onDelete(selectedRecord) {
            this.selectedRecord = selectedRecord
            this.$bvModal.show('deleteRecordModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>