<div class="mainConatiner">
    <div class="headerContainer">
        <h1>Enviromaster</h1>
        <p>Dashboard</p>
        <button><i class="fa-solid fa-floppy-disk fa-bounce"></i><p>Save</p></button>
    </div>
    <main>
        <div class="enterJob">
            <input type="text" placeholder="Enter Job Number" />
            <button>ADD</button>
        </div>
    </main>
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

.enterJob {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px;
    background-color: white;
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