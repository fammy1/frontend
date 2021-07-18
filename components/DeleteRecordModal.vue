<template>
    <div>
        <b-modal id="deleteRecordModal" title="Delete Record" ok-title="Delete Record" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this record? <br><br>
            Name: {{record.name}} <br>
            Age: {{record.age}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        record: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/records/' + this.record.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>