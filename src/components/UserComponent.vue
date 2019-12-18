<template>
    <div style="margin-top: 1.5rem">
        <h1 class="subtitle">Users</h1>
        <div class="field has-addons">
            <div class="control">
                <input class="input" type="text" placeholder="Find user" v-model="searchTerm">
            </div>
            <div class="control is-expanded">
                <div class="select is-fullwidth">
                    <select v-model="fieldName">
                        <option value="name">Name</option>
                        <option value="alias">Alias</option>
                        <option value="email">Email</option>
                        <option value="phone">Phone</option>
                    </select>
                </div>
            </div>
            <div class="control">
                <a class="button is-success" @click.prevent="search">
                    Search
                </a>
            </div>
        </div>
        <user-box-component :user="user" v-for="user in filteredUsers" :key="user._id"></user-box-component>
    </div>
</template>

<script>
    import UserBoxComponent from './UserBoxComponent.vue'

    export default {
        name: 'user-component',
        components: {
            UserBoxComponent,
        },
        props: {
            users: Array,
        },
        methods: {
            search() {
                this.filteredUsers = this.users.filter(user => {
                    return user[this.fieldName] == this.searchTerm
                })
            }
        },
        data() {
            return {
                filteredUsers: [],
                searchTerm: '',
                fieldName: 'name',
            }
        }
    }
</script>