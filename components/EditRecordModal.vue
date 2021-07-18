<template>
    <div>
        <b-modal id="editRecordModal" title="Edit Record" ok-title="Save Record" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="record.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Age" label-for="age">
                <b-form-input id="age" v-model="record.age" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Skills" label-for="skills">
                <b-form-input id="skills" v-model="record.skills" trim></b-form-input>
                </b-form-group>


                <b-form-group label="Address" label-for="address">
                <b-form-input id="address" v-model="record.address" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Designation" label-for="designation">
                <b-form-select v-model="record.designation" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        record: {}
    },
    data() {
        return {
            options: [
                {value: 'programmer', text: 'programmer'},
                {value: 'designer', text: 'designer'},
               
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/records/' + this.record.id, this.record)
            .then((res)=>{
                if(res.status==202) {
                    alert('Edit successful!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>