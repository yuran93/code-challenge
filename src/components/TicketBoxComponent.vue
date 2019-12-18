<template>
    <div class="box">
        <table class="table">
            <tr>
                <td colspan="2">
                    <strong>{{ ticket.subject }}</strong>
                </td>
            </tr>
            <tr>
                <td>Description</td>
                <td>{{ ticket.description }}</td>
            </tr>
            <tr>
                <td>Priority</td>
                <td>{{ ticket.priority }}</td>
            </tr>
            <tr>
                <td>Status</td>
                <td>{{ ticket.status }}</td>
            </tr>
            <tr>
                <td>Due At</td>
                <td>{{ ticket.due_at }}</td>
            </tr>
            <tr>
                <td>Tags</td>
                <td>{{ ticket.tags.join(', ') }}</td>
            </tr>
            <tr>
                <td>Assignee</td>
                <td>{{ ticket.assignee ? ticket.assignee.name : '-' }}</td>
            </tr>
            <tr>
                <td>Submitter</td>
                <td>{{ ticket.submitter ? ticket.submitter.name : '-' }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'ticket-box-component',
        props: {
            ticket: Object,
        },
    }
</script>