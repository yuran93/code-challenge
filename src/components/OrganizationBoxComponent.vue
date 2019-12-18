<template>
    <div class="box">
        <table class="table">
            <tr>
                <td colspan="2">
                    <strong>{{ organization.name }}</strong>
                </td>
            </tr>
            <tr>
                <td>Details</td>
                <td>{{ organization.details }}</td>
            </tr>
            <tr>
                <td>Domains</td>
                <td>{{ organization.domain_names.join(', ') }}</td>
            </tr>
            <tr>
                <td>Tags</td>
                <td>{{ organization.tags.join(', ') }}</td>
            </tr>
            <tr>
                <td>Users</td>
                <td>
                    <p v-for="user in organization.users" :key="user._id">{{ user.name }}</p>
                </td>
            </tr>
            <tr>
                <td>Tickets</td>
                <td>
                    <p v-for="ticket in organization.tickets" :key="ticket._id">{{ ticket.subject }}</p>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'organization-box-component',
        props: {
            organization: Object,
        },
    }
</script>