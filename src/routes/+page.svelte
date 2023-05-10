<script>
    let edit=false
    let users=[
        {
        id:0,
        name:"Gordon",
        age:20,
        country:"Spain"

    },
    {
        id:1,
        name:"James",
        age:40,
        country:"Italy"

    }
    ]

    //empty obj

    let data={
        id:null,
        name:"",
        age:"",
        country:""

    }
    const createUser=(e)=>{
        e.preventDefault()
        const newUser={
            id:Date.now()+Math.random(),
            name:data.name,
            age:data.age,
            country:data.country
        }
        console.log(newUser.id)
        users=users.concat(newUser)

        //reset form
        data={
        id:null,
        name:"",
        age:"",
        country:""

    }

    }
    const deleteUser=(id)=>{
        //filter method
        users=users.filter((user)=>user.id!==id)
    }
    const editUser=(user)=>{
        edit=true
        data=user
    }
    const updateUser=()=>{
        edit=!edit
        let userDB={
            name:data.name,
            age:data.age,
            country:data.country,
            id:data.id
        }

        //find Index no

        let objIndex=users.findIndex((obj)=>obj.id==userDB.id)
        users[objIndex]=userDB
        data={
            id:null,
            name:"",
            age:"",
            country:""
        }

    }
</script>

<main>
 <h2>Create User</h2>

<form>
    <label for="name">Name</label>
    <input bind:value={data.name} type="text" placeholder="Enter name">
    <label for="age">Age</label>
    <input bind:value={data.age} type="number" placeholder="Enter age">
    <label for="country">Country</label>
    <input bind:value={data.country} type="text" placeholder="Enter country">
    {#if edit===false}
    <button on:click={createUser}>Add User</button>
    {:else}
    <button on:click={updateUser}>Update User</button>
    {/if}

</form>


 {#each users as user}
 <br>
    <div style="display:inline">{user.name} is {user.age} years old and he is from {user.country}</div>
    <button on:click={()=>editUser(user)}>Edit User </button>
    <button on:click={()=>deleteUser(user.id)}>Delete User</button>
 {/each}



</main>

<style>

</style>