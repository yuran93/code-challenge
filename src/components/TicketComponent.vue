<template>
    <div style="margin-top: 1.5rem">
        <h1 class="subtitle">Tickets</h1>
        <div class="field has-addons">
            <div class="control is-expanded">
                <input class="input" type="text" placeholder="Find ticket" v-model="searchTerm">
            </div>
            <div class="control">
                <a class="button is-success" @click.prevent="search">
                    Search
                </a>
            </div>
        </div>
        <ticket-box-component 
            v-for="ticket in filteredTickets" 
            :ticket="ticket" 
            :key="ticket._id"></ticket-box-component>
    </div>
</template>

<script>
    import TicketBoxComponent from './TicketBoxComponent.vue'

    export default {
        name: 'ticket-component',
        components: {
            TicketBoxComponent,
        },
        props: {
            tickets: Array,
        },
        methods: {
            search() {
                this.filteredTickets = this.tickets.filter(ticket => {
                    return ticket.subject.includes(this.searchTerm)
                })
            }
        },
        data() {
            return {
                filteredTickets: [],
                searchTerm: '',
                fieldName: 'name',
            }
        }
    }
</script>