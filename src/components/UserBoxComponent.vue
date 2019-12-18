<template>
    <div class="box">
        <table class="table">
            <tr>
                <td colspan="2">
                    <strong>{{ user.name }}</strong>
                </td>
            </tr>
            <tr>
                <td>Alias</td>
                <td>{{ user.alias }}</td>
            </tr>
            <tr>
                <td>Email</td>
                <td>{{ user.email }}</td>
            </tr>
            <tr>
                <td>Phone</td>
                <td>{{ user.phone }}</td>
            </tr>
            <tr>
                <td>Signature</td>
                <td>{{ user.signature }}</td>
            </tr>
            <tr>
                <td>Organization</td>
                <td>{{ user.organization ?  user.organization.name : '-' }}</td>
            </tr>
            <tr>
                <td>Submitted Tickets</td>
                <td>
                    <p v-for="ticket in user.submittedTickets" :key="ticket._id">{{ ticket.subject }}</p>
                </td>
            </tr>
            <tr>
                <td>Assigned Tickets</td>
                <td>
                    <p v-for="ticket in user.assignedTickets" :key="ticket._id">{{ ticket.subject }}</p>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'user-component',
        props: {
            user: Object,
        },
    }
</script>