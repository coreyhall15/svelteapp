<script>
    import {onMount} from 'svelte'
    import { auth, db } from "../lib/firebase/firebase"
    import {doc, getDoc} from 'firebase/firestore'
    import {authStore} from "../store/store"

    const nonAuthRoutes = ['/', 'product']

    onMount(() => {
        console.log('mounted')
        const unsubscribed = auth.onAuthStateChanged(async (user) => {
            const currentPath = window.location.pathname;

            if (!user && !nonAuthRoutes.includes(currentPath)) {
            window.location.href = '/'
            return
        }
            if (user && currentPath == '/') {
            window.location.href = '/dashboard'
            return
        }
            

            let dataToSetToStore
            const docRef = doc(db, 'users', user.uid)
            const docSnap = await getDoc(docRef)
            if (!docSnap.exists()) {
                const userRef = doc(db, 'user', user.uid)
                dataToSetToStore = {
                    email: user.email,
                    name: user.displayName,
                }
                await setDoc(userRef, dataToSetToStore, {merge: true});
                
            }else{
                const userData = docSnap.data()
                dataToSetToStore = userData
                }
                authStore.update(curr => {
                    return {
                        user,
                        data: dataToSetToStore,
                        loading: false,
                    }
                })
            }
    )})
                
        
    
    
</script>


<div class="mainContainer">

    <slot/>
</div>

<style>
.mainContainer {
    min-height: 100vh;
    background: linear-gradient(to right, #000428, #000046);
    color: white;
    display: flex;
    position: relative;
    flex-direction: column;

}
</style>