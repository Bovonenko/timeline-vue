<template>
	<div class="app">
		<user-form @create="createNewUser" />
		<div class="wrapper" v-if="!isUserLoading && !error && users.length > 0">
			<user-list 
				:users="users" 
			/>
		</div>
		<my-spinner v-if="isUserLoading"/>
		<my-error v-if="error"/>
		<h2 v-if="!users.length > 0" class="text-center text-danger mt-5" >Users list is empty</h2>
	</div>
	
</template>

<script>
import UserList from './components/UserList.vue' ;
import UserForm from './components/UserForm.vue';
import MySpinner from './components/UI/MySpinner.vue';
import MyError from './components/UI/MyError.vue';

export default {
  name: 'App',
  components: { UserList, UserForm, MySpinner, MyError },
  data() {
    return {
      users: [],
	  isUserLoading: false,
	  error: false
    }
  },
  methods: {
    async fetchUsers() {
		try {
			this.isUserLoading = true;
			const res = await fetch('../timeline.json');

			this.users = await res.json();
		} catch (e) {
			this.error = true;
			alert('Error')

		} finally {
			this.isUserLoading = false;
		}
     
    },
    sortUsersByDate(arr) {
      arr.sort((a, b) => {
        return new Date(a.registered) - new Date(b.registered)
      })
    },
	createNewUser(newUser) {
		this.users.push(newUser);
	}
  },
  async mounted() {
    await this.fetchUsers();
	this.sortUsersByDate(this.users)
  },
  watch: {
	users(newValue) {
		console.log(newValue)
	}
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');

*{
	margin:0;
	padding:0;
	box-sizing: border-box;
}
body {
	background-color: #f9fafb;
	font-family: 'Lato', sans-serif;
	min-height: 100vh;
	padding: 60px 15px;
}

.wrapper {
	position: relative;
	max-width: 1000px;
    margin: auto;
	margin-top: 60px;
	&::after,&::before {
		content: '';
		width: 20px;
		height: 20px;
		background-color: #0a5084;
		position: absolute;
		border-radius: 100%;
		left: calc(50% - 10px);
	}
	&::after {
		bottom: 0;
	}
	
}

/* responsive */
@media(max-width: 767px){
	form {
		width: 70%;
	}
	.wrapper {
		&::after,&::before {
			left: -1px;
		}
	}
	
	.timeline::before{
		left: 7px;
	}
	.item{
		&__date {
			font-size: 15px;
		}
		&__content {
			h3 {
				font-size: 16px;
			}
			p {
				font-size: 13px;
			}
		}
		&:nth-child(odd) {
			padding-right: 0;
			text-align: left;
		}
		&:nth-child(odd),&:nth-child(even) {
			padding-left: 37px;
			.item__content::after {
				left: -24px;
			}
			.dot{
				left: -39px;
				top: calc(50% - 10spx);
			}
		}
	}
	
}
</style>
