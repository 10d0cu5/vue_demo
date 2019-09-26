<template>
    <div>
        <h1>Hi {{account.user.name}}!</h1>
        <em v-if="users.loading">Loading users...</em>
        <span v-if="users.error" class="text-danger">ERROR: {{users.error}}</span>
        <div v-if="users.items">
            <div v-for="item in users.items">
                <p v-for="element in item">
                    {{element.id}}
                    {{element.name}}
                    {{element.email}}
                </p>
            </div> 
        </div>
        <p>
            <router-link to="/login">Logout</router-link>
        </p>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState({
            account: state => state.account,
            users: state => state.users.all
        })
    },
    created () {
        this.getAllUsers();
    },
    methods: {
        ...mapActions('users', {
            getAllUsers: 'getAll',
            deleteUser: 'delete'
        })
    }
};
</script>