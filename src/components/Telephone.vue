<template>

    
    <div>
      <div class="keypad">
        <button v-for="n in ['1', '2', '3', '4', '5', '6', '7', '8', '9', '*', '0', '#']" :key="n" @click="addNumber(n)">{{ n }}</button>
      </div>
      <div>
        <input type="text" v-model="number" readonly />
      </div>
      
      <div>
        <button @click="searchContact">Rechercher contact</button>
      </div>
      <div>
        <button @click="call">Appeler</button>
      </div>
      <div>
        <h3>Journal d'appels</h3>
        <table>
          <tr>
            <th>Numéro</th>
            <th>Nom</th>
            <th>Date</th>
          </tr>
          <tr v-for="call in callLog" :key="call.date">
            <td>{{ call.number }}</td>
            <td>{{ call.name }}</td>
            <td>{{ call.date }}</td>
          </tr>
        </table>
      </div>
    </div>
  </template>
  
  
  
  <script>
  export default {
    data() {
      return {
        number: '',
        contactName: '',
        contacts: [
          { name: 'John Doe', number: '1234567890' },
          { name: 'Jane Smith', number: '0987654321' }
        ],
        callLog: []
      }
    },
  
    methods: {
      addNumber(n) {
        this.number += n;
      },
      searchContact() {
        let contact = this.contacts.find(c => c.number === this.number);
        if (contact) {
          this.contactName = contact.name;
        } else {
          this.contactName = '';
        }
      },
  
      call() {
        let call = {
          number: this.number,
          name: this.contactName,
          date: new Date()
        }
        this.callLog.unshift(call);
        this.number = '';
        this.contactName = '';
      }
    }
  
  
  
  }
  </script>
  
  
  <style>
  .keypad {
    display: flex;
    flex-wrap: wrap;
  }
  
  .key {
    width: 33%;
    height: 50px;
    border: 1px solid #ccc;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .display {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: center;
  }
  </style>
  
  
    
  
  