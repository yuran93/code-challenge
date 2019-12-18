<template>
    <div id="app" class="container">
        <div class="columns">
            <div class="column is-4">
                <organization-component :organizations="mappedOrganizations"></organization-component>
            </div>
            <div class="column is-4">
                <ticket-component :tickets="mappedTickets"></ticket-component>
            </div>
            <div class="column is-4">
                <user-component :users="mappedUsers"></user-component>
            </div>
        </div>
    </div>
</template>

<script>
    import OrganizationComponent from './components/OrganizationComponent.vue'
    import TicketComponent from './components/TicketComponent.vue'
    import UserComponent from './components/UserComponent.vue'

    export default {
        name: 'app',
        components: {
            OrganizationComponent,
            TicketComponent,
            UserComponent,
        },
        data() {
            return {
                mappedOrganizations: [],
                mappedTickets: [],
                mappedUsers: [],

                organizations: [],
                tickets: [],
                users: [],
            }
        },
        methods: {

            // Fetches and data from json.
            async fetchJson(filename) {

                let response = await this.$http.get(filename)
                        
                if (response) {
                    return response.data
                }       

                // We'll log any issues.
                console.log(response)

                return false
            },

            // Create mapped organization object.
            getMappedOrganizationObject(organization) {

                let mappedOrganization = {...organization}

                mappedOrganization.tickets = this.tickets.filter(ticket => {
                    return ticket.organization_id == organization._id
                })

                mappedOrganization.users = this.users.filter(user => {
                    return user.organization_id == organization._id
                })

                return mappedOrganization

            },

            // Create mapped ticket object.
            getMappedTicketObject(ticket) {

                let mappedTicket = {...ticket}

                mappedTicket.assignee = this.users.filter(user => {
                    return ticket.assignee_id == user._id
                })[0]

                mappedTicket.submitter = this.users.filter(user => {
                    return user.submitter_id == user._id
                })[0]

                mappedTicket.organization = this.organizations.filter(organization => {
                    return ticket.organization_id == organization._id
                })[0]

                return mappedTicket

            },

            // Create mapped user object.
            getMappedUserObject(user) {

                let mappedUser = {...user}

                mappedUser.assignedTickets = this.tickets.filter(ticket => { 
                    return ticket.assignee_id == user._id 
                })

                mappedUser.submittedTickets = this.tickets.filter(ticket => {
                    return ticket.submitter_id == user._id
                })

                mappedUser.organization = this.organizations.filter(organization => {
                    return user.organization_id == organization._id
                })[0]

                return mappedUser

            },

            // We'll map organizations, tickets and users.
            async mapJsonObjects() {

                this.organizations = await this.fetchJson('./assets/organizations.json')
                this.tickets = await this.fetchJson('./assets/tickets.json')
                this.users = await this.fetchJson('./assets/users.json')

                // We'll just map the organizations here.
                this.organizations.forEach(organization => {
                    this.mappedOrganizations.push(this.getMappedOrganizationObject(organization))
                })

                // Map the tickets here.
                this.tickets.forEach(ticket => {
                    this.mappedTickets.push(this.getMappedTicketObject(ticket))
                })

                // Map the usres here.
                this.users.forEach(user => {
                    this.mappedUsers.push(this.getMappedUserObject(user))
                })

            }
        },

        mounted() {
            this.mapJsonObjects()
        }
    }
</script>

<style>

</style>