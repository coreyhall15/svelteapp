<script>
    let enterJob = ["Chops Lobster Bar"];
    let currentJob = '';
    let error = false;

    function addJob (){
            error = false;
            if (!currentJob) {
                error = true;
            }
            enterJob = [...enterJob, currentJob];
            currentJob = "";
        }

        function editJob(index) {
            let newJob = enterJob.filter((val, i) => {
                return i !== index;
                })
                currentJob = enterJob[index];
                enterJob = newJob;
            }
            

        function deleteJob(index) {
            let newJob = enterJob.filter((val, i) => {
                return i !== index;
                })
                enterJob = newJob;
        }
    

</script>

<div class="mainConatiner">
    <div class="headerContainer">
        <h1>Enviromaster</h1>
        <p>Dashboard</p>
        <div class="headerButtons">
        <button><i class="fa-solid fa-user-circle fa-bounce"></i><p>Profile</p></button>
        <button><i class="fa-solid fa-floppy-disk fa-bounce"></i><p>Save</p></button>
        <button><i class="fa-solid fa-sign-out fa-bounce"></i><p>Logout</p></button>
        </div>
    </div>
    <main>
        {#if enterJob.length === 0} 
            <p>
                There are no jobs
            </p>
        {/if}
        
        {#each enterJob as job, index }
        <div class="job">
            <p>
            {index+1}. {job}
        </p>
        <div class="actions">
        <i on:click={() => {
            editJob(index);
        }} 
        on:keydown={() => {}}
        class="fa-solid fa-pen"/>
        <i on:click={() => {
            deleteJob(index);
        }} 
        on:keydown={() => {}} class="fa-solid fa-trash-can"/>
        </div>
        </div>
        {/each}
        
       
    </main>
         <div class={"enterJob" + (error ? 'errorBorder' : "")}>
        <input bind:value={currentJob} type="text" placeholder="Enter Job" />
        <button on:click={addJob}>ADD</button>
        </div>
</div>

<style>
.mainConatiner {
    display: flex;
    flex-direction: column;
    height: 100vh;
    width: 100vw;

}

.headerContainer {
    display: flex;
    align-items: center;
    justify-content: space-between;

    
}

.headerButton {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
}

.headerContainer button {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 14px;
    margin: 4px 2px;
    cursor: pointer;
    gap: 8px;
}

.headerContainer button i {
    font-size: 1.2rem;
}

.headerContainer button:hover {
    opacity: 0.7;
    cursor: pointer;

}

main {
    display: flex;
    flex-direction: column;
    background-color: gray;
    gap: 8px;
}

.job {
    border: left solid black;
    padding: 8px 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.actions {
    display: flex;
    gap: 14px;
    align-items: 8px;
    font-size: 1.3rem;
}

.actions i:hover {
    cursor: pointer;
    color:coral

}

.enterJob {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px;
    background-color: white;
}

.errorBorder {
    border-color: coral !important;
}

.enterJob button {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
}
</style>