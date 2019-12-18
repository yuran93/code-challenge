<template>
    <div style="margin-top: 1.5rem">
        <h1 class="subtitle">Organizations</h1>
        <div class="field has-addons">
            <div class="control">
                <input class="input" type="text" placeholder="Find organization" v-model="searchTerm">
            </div>
            <div class="control is-expanded">
                <div class="select is-fullwidth">
                    <select v-model="fieldName">
                        <option value="name">Name</option>
                    </select>
                </div>
            </div>
            <div class="control">
                <a class="button is-success" @click.prevent="search">
                    Search
                </a>
            </div>
        </div>
        <organization-box-component 
            v-for="organization in filteredOrganizations" 
            :organization="organization" 
            :key="organization._id"></organization-box-component>
    </div>
</template>

<script>
    import OrganizationBoxComponent from './OrganizationBoxComponent.vue'

    export default {
        name: 'organization-component',
        components: {
            OrganizationBoxComponent,
        },
        props: {
            organizations: Array,
        },
        methods: {
            search() {
                this.filteredOrganizations = this.organizations.filter(organization => {
                    return organization[this.fieldName] == this.searchTerm
                })
            }
        },
        data() {
            return {
                filteredOrganizations: [],
                searchTerm: '',
                fieldName: 'name',
            }
        }
    }
</script>