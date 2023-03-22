<template>
  <div>
    <h2>Inventory</h2>
    <div class="container-inv">
      <ul class="card-list">
        <li class="card-item" v-for="(item, index) in userInventory" :key="index">
          <div class="card-container">
            <img :src="item.cardImg" alt="card image">
            <p class="card-name">{{ item.cardName }}</p>
            <button @click="deleteItem(item)">Delete</button> <!-- Add a button to delete the item -->
          </div>
         
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import firebase from 'firebase/app';
import 'firebase/firestore';

export default {
  data() {
    return {
      userInventory: []
    }
  },
  created() {
    const db = firebase.firestore();
    const user = firebase.auth().currentUser;
    if (user) {
      db.collection("inventory").where("userId", "==", user.uid).get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          this.userInventory.push({...doc.data(), id: doc.id}); // Include the document ID in the userInventory array
        });
      });
    }
  },
  methods: {
    async deleteItem(item) {
      const collectionName = "inventory"; // Replace with the name of your Firestore collection
      const documentId = item.id; // Use the document ID to delete the item
      try {
        const db = firebase.firestore();
        const docRef = db.collection(collectionName).doc(documentId);
        await docRef.delete();
        console.log(`Document with ID ${documentId} successfully deleted from Firestore`);
        // Remove the deleted item from the userInventory array
        this.userInventory = this.userInventory.filter((invItem) => invItem.id !== item.id);
      } catch (error) {
        console.error("Error deleting document: ", error);
      }
    }
  }
}
</script>
  
  <style scoped>
  /* .inventory{
    display: block;
  text-align: center;
  width: 210px;
  margin-left: 20px;
  margin-bottom: 20px;
  border: 3px red solid;
  border-radius: 12px;
  overflow:hidden;
  }
  .inventory img {
    height: 150px;
  }
 .container-inv{
    display: inline-flex;
    flex-direction: column 1fr 1fr 1fr;
    flex-wrap: wrap;
 } */
 .card-list {
    display: flex;
    flex-wrap: wrap;
    list-style: none;
    margin: 0;
    padding: 0;
  }
  
  .card-item {
    flex: 1 1 20%;
    margin: 10px;
    border: 2px solid rgb(199, 8, 8);
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    transition: transform 0.5s;
    cursor: pointer;
  }
  
  .card-item:hover {
    transform: translateY(-5px);
  }
  
  .card-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px;
    width: 200px;
  }
  
  .card-name {
    font-size: 1.2rem;
    text-align: center;
    margin-top: 10px;
  }
  
  .card-name::before,
  .card-name::after {
    content: "";
    display: block;
    height: 1px;
    background-color: #ccc;
    width: 50%;
    margin: 5px 0;
  }
  
 img {
    height: 150px;
  }
</style>