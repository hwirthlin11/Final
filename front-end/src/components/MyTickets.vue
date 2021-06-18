<template>
<div class="main">
<button @click="setCreating" class="buttonClass" id = "newProblem">
  Click to report a new problem.
</button>
  <h2>{{user.firstName}} <button @click="logout" class="buttonClass buttonClass1"> -> Logout?</button></h2>
  <h1>My Flower Problems: </h1>
  <div>
</div>
<form class="submitButton" v-if="creating" @submit.prevent="addTicket">
  <legend>Describe your problem for us.</legend>
  <fieldset>
    <textarea v-model="flowers" placeholder="Type of Flower(s)"></textarea>
    <textarea v-model="problem" placeholder= "Problem"></textarea>
    <br />
    <button @click="cancelCreating" class="buttonClass space-right">Cancel</button>
    <button class="buttonClass buttonClass1" type="submit">Submit</button>
  </fieldset>
</form>
<div v-for="ticket in tickets" v-bind:key="ticket.id">
  <div class="ticket">
    <div class="problem">
      <h3> Problem reported on {{time(ticket.created)}}</h3>
      <p>{{ticket.problem}}</p>
      <p>{{ticket.flowers}}</p>
      <h1 v-if="ticket.response"><i>{{ticket.response}}</i></h1>
      <p class = "response" v-else><i>Currently weeding. We'll check back here soon!</i></p>
    </div>
  </div>
</div>
</div>
</template>
<script>
import axios from 'axios';
import moment from 'moment';
export default {
  name: 'MyTickets',
  data() {
    return {
      creating: false,
      problem: '',
      flowers: '',
      tickets: [],
    }
  },
  computed: {
    user() {
      return this.$root.$data.user;
    }
  },
  created() {
  this.getTickets();
},
  methods: {
  async logout() {
    try {
      await axios.delete("/api/users");
      this.$root.$data.user = null;
    } catch (error) {
      this.$root.$data.user = null;
    }
  },
  async getTickets() {
    try {
      let response = await axios.get("/api/tickets");
      this.tickets = response.data.tickets;
      return true;
    } catch (error) {
      console.log(error);
    }
  },
  time(d) {
  return moment(d).format('D MMMM YYYY, h:mm:ss a');
},
setCreating() {
  this.creating = true;
},
cancelCreating() {
  this.creating = false;
},
async addTicket() {
  try {
    await axios.post("/api/tickets", {
      problem: this.problem
    });
    this.problem = "";
    this.creating = false;
    this.getTickets();
    return true;
  } catch (error) {
    console.log(error);
  }
}
}
}
</script>
<style scoped>
.main h1{
  text-align: left;
  font-size:30px;
  color: #797b84;
}
.main{
text-align:center;
}
textarea {
  width: 100%;
  max-width: 500px;
}
h2{
  font-size: 30px;
  font-weight:bold;
  text-align: right;
}
.ticket{
  text-align: left;
}
.ticket p {
  font-size:14px;
}
h3 {
  font-size: 16px;
  font-weight: normal;
  background-color: #467599;
  width: 500px;
  padding: 10px 20px;
  color:white;
}
.response{
color:#9dadad;
}

label {
  background-color: #023047;
  color: white;
  padding: 5px;
  border-radius: 30px;
  font-size: 12px;
  margin-right: 10px;
}
#newProblem{
  font-size:20px;
  background-color:#457b9d;
  color:#dbdcd7;
}

.ticket {}
</style>
