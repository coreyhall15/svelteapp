<script>
    let email = '';
    let password = '';
    let confirmPassword = '';
    let error = false;
    let register = false;

    function handleAuthenticate() {
        if ( ! email || password || (register && !confirmPassword)) {
            error = true
            return
        }
    }

    function handleRegister() {
        register = !register;
    }

</script>



 <div class="authContainer">
    <form>
        <h1>{register ? "Register" : "Login"}</h1>
        {#if error} 
        <p class="error">The information entered is not correct</p>
        {/if}
        <label>
            <p class={email ? ' above ' : ' center'}>Email</p>
            <input bind:value={email} type="email" placeholder="email" />
        </label>
        
        <label>
            <p class={password ? ' above ' : ' center'}>Password</p>
            <input bind:value={password} type="password" placeholder="PASSWORD" />
        </label>

        {#if register}
        <label>
            <p class={confirmPassword ? ' above ' : ' center'}>Confirm Password</p>
            <input bind:value={confirmPassword} type="password" placeholder="Confirm PASSWORD"/>
        </label>
        {/if}
        <label>
            <p class={confirmPassword ? ' above ' : ' center'}>Confirm Password</p>
            <input bind:value={confirmPassword} type="password" placeholder="Confirm PASSWORD"/>
        </label>

        <button type="button">SUBMIT</button>
    </form>

    <div class="options">
        <p>Or</p>
        {#if register}
        <div>
            <p>Already have an account<p/>
            <p on:click={handleRegister} on:keydown={ () => {} }>Login</p>
        </div>
        {:else}

        <p>Dont have an account<p/>
            <p on:click={handleRegister} on:keydown={ () => {} }>Register</p>

        {/if}

    </div>
 </div>

 <style>
    .authContainer {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        flex: 1;
        padding: 24px;
        
        
    }

    form {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 14px;
        width: 400px;
        max-width: 100%;
        margin: 0 auto;
    }

    form input {
        width: 100%;

    }

    h1 {
        text-align: center;
        font-size: 3rem;
    }

    form label {
        position: relative;
        border: 2px solid white;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: center;
        width: 100%;
        gap: 4px;
    }

    form input {
        border: none;
        background: transparent;
        color: white;
        padding: 14px 14px;

    }

    form input:focus {
        border: none;
        outline: none;
    }

    form label:focus-within {
        border-color: blue;
    }

    form button {
        background: aliceblue;
        color: gray;
        border: none;
        padding: 14px 14px;
        cursor: pointer;
        font-size: 1.2rem;
    }

    form button:hover {
        background: #f2f2f2;
    }

    .above,
    .center {
    
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateY(-50%);
        pointer-events: none;
        border-radius: 4px;
        padding: 0 4px;
        font-size: 0.8rem;
        color: white;
       
    }

    .above {
        top: 0;
        left: 24px;
        background: #333;
        border: 1px solid blue;
    }

    .center {
        top: 50%;
        left: 6px;
        border: 1px solid transparent;
        opacity: 0;
    }

    .error {
        color: red;
        font-size: 0.9rem;
    }

    .options {
        padding: 14px 0;
        overflow: hidden;
        width: 100%;
        

    }

    .options > p {
        position: relative;
        text-align: center;
        width: fit-content;
        margin: 0 auto;
    }

    .options > p::after,
    .options > p::before {
        content: '';
        position: absolute;
        top: 50%;
        left: 0%;
        transform: translateY(-50%);
        width: 100vm;
        height: 1px;
        background: white;
    }
    
    .options > p::after {
        right: 100%;
    }

    .options > p::before {
        left: 100%;
    }
    
 </style>