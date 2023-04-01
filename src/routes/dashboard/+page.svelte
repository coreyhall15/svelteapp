<script>
    import { db } from "../../lib/firebase/firebase";
    import { doc, setDoc, updateDoc } from "firebase/firestore";
    import { authHandlers, authStore } from "../../store/store";
    import { onMount } from "svelte";
  
    let contacts = [];
    let name = "";
    let address = "";
    let email = "";
    let notes = "";
    let error = false;
    let editingIndex = -1; // initialize editingIndex to -1
  
    authStore.subscribe((curr) => {
      contacts = curr.data.contacts;
    });
  
  
    async function addContact() {
      error = false;
      if (!name || !address || !email) {
        error = true;
        return;
      }
      const newContact = { name, address, email, notes };
      contacts.push(newContact);
      await saveContacts();
      name = "";
      address = "";
      email = "";
      notes = "";
    }
  
    async function updateContact() {
      const userRef = doc(db, "users", authStore.user.uid);
      await updateDoc(userRef, {
        [`contacts.${editingIndex}.name`]: name,
        [`contacts.${editingIndex}.address`]: address,
        [`contacts.${editingIndex}.email`]: email,
        [`contacts.${editingIndex}.notes`]: notes,
      });
      editingIndex = -1;
      name = "";
      address = "";
      email = "";
      notes = "";
    }
  
    async function deleteContact(index) {
      const newContacts = [...contacts.slice(0, index), ...contacts.slice(index + 1)];
      const userRef = doc(db, "users", authStore.user.uid);
      await setDoc(userRef, { contacts: newContacts }, { merge: true });
    }
  
    async function saveContacts() {
      const userRef = doc(db, "users", authStore.user.uid);
      await setDoc(userRef, { contacts }, { merge: true });
    }
  
    function editContact(index) {
      editingIndex = index;
      name = contacts[index].name;
      address = contacts[index].address;
      email = contacts[index].email;
      notes = contacts[index].notes;
    }
  
    function clearForm() {
      editingIndex = -1;
      name = "";
      address = "";
      email = "";
      notes = "";
    }
  </script>
  
  <form on:submit|preventDefault={editingIndex === -1 ? addContact : updateContact}>
    <label>
      Name:
      <input type="text" bind:value={name} />
    </label>
    <label>
      Address:
      <input type="text" bind:value={address} />
    </label>
    <label>
      Email:
      <input type="email" bind:value={email} />
    </label>
    <label>
      Notes:
      <textarea bind:value={notes}></textarea>
    </label>
    
  </form>
  
  
  <!-- <ul> -->
    {#each contacts as contact, index}
      <li>
        <strong>{contact.name}</strong>
        <button on:click={() => editContact(index)}>Edit</button>
        <button on:click={() => deleteContact(index)}>Delete</button>
        <br />
        {contact.address}<br />
        {contact.email}<br />
        {contact.notes}
      </li>
    {/each}
  
        
    
  
  
  <div class="form-container">
    <div class="form-row">
      <label for="name">Name:</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-row">
      <label for="address">Address:</label>
      <input type="text" id="address" bind:value={address} />
    </div>
    <div class="form-row">
      <label for="email">Email:</label>
      <input type="email" id="email" bind:value={email} />
    </div>
    <div class="form-row">
      <label for="notes">Notes:</label>
      <textarea id="notes" bind:value={notes}></textarea>
    </div>
    <div class="form-row">
      {#if editingIndex === -1}
        <button on:click={addContact}>Add</button>
      {:else}
      <!-- {error && <p>Please fill out all required fields</p>} -->
      <button type="submit">{editingIndex === -1 ? "Add" : "Update"}</button>
      <!-- {editingIndex !== -1 && <button type="button" on:click={clearForm}>Cancel</button>} -->
      {/if}
    </div>
    </div>
    
  
    <div class="container">
        <h1>Contacts List</h1>
        <form class="form" on:submit|preventDefault={deleteContact ? updateContact : addContact}>
          <input type="text" placeholder="Name" bind:value={name} required />
          <input type="text" placeholder="Address" bind:value={address} required />
          <input type="email" placeholder="Email" bind:value={email} required />
          <textarea placeholder="Notes" bind:value={notes}></textarea>
          <button type="submit">{deleteContact ? 'Update' : 'Add'}</button>
        </form>

        <div class="contacts">
            {#if contacts && contacts.length}
                {#each contacts as contact, index}
                    <div class="contact">
                    <h3>{contact.name}</h3>
                    <p>{contact.address}</p>
                    <p>{contact.email}</p>
                    <p>{contact.notes}</p>
                    <button class="edit" on:click={() => editContact(index)}>Edit</button>
                    <button class="delete" on:click={() => deleteContact(index)}>Delete</button>
                    </div>
                {/each}
            {:else}
                <p>No contacts found.</p>
            {/if}
        </div>
        
        </div>
<style>
    .form-container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    
    .form-row {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 5px;
    }
    
    .form-row label {
        margin-bottom: 5px;
    }
    
    .form-row input, .form-row textarea {
        padding: 5px;
        width: 300px;
    }
    
    .form-row button {
        margin-top: 10px;
    }
    
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    
    .form {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 20px;
        border: 1px solid black;
        padding: 10px;
        width: 300px;
    }
    
    .form input, .form textarea {
        margin: 5px;
        padding: 5px;
        width: 100%;
    }
    
    .form button {
        margin-top: 10px;
    }
    
    .contacts {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 20px;
        border: 1px solid black;
        padding: 10px;
        width: 300px;
    }
    
    .contact {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 5px;
        padding: 5px;
        border: 1px solid black;
        width: 100%;
    }
    
    .contact button {
        margin: 5px;
    }
    
    .contact button.edit {
        background-color: green;
    }
    
    .contact button.delete {
        background-color: red;
    }
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .form {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
    border: 1px solid black;
    padding: 10px;
    width: 300px;
  }

  .form input, .form textarea {
    margin: 5px;
    padding: 5px;
    width: 100%;
  }

  .form button {
    margin-top: 10px;
  }

  .contacts {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
    border: 1px solid black;
    padding: 10px;
    width: 300px;
  }

  .contact {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 5px;
    padding: 5px;
    border: 1px solid black;
    width: 100%;
  }

  .contact button {
    margin-top: 5px;
  }

</style>
