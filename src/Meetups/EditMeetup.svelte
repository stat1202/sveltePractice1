<script>
    import {createEventDispatcher} from "svelte"
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import Modal from "../UI/Modal.svelte";

    let title = ""
    let subtitle = "" 
    let address = ""
    let email ="" 
    let description = "" 
    let imageUrl = ""

    const dispatch = createEventDispatcher()
    function submitForm() {
        dispatch("save", {
            title: title,
            subtitle: subtitle,
            address: address,
            email: email,
            description: description,
            imageUrl: imageUrl
        })
    }

    function cancel(){
        dispatch('cancel')
    }
</script>

<style>
    form{
        width:100%;
    }
</style>

<Modal title="Edit Meetup Data" on:cancel>
    <form on:submit|preventDefault="{submitForm}">
        <TextInput label ="Title" id="title" value={title} on:input="{(event)=> title = event.target.value}" />
        <TextInput label ="Subitle" id="subtitle" value={subtitle} on:input="{(event)=> subtitle = event.target.value}" />
        <TextInput label ="Address" id="address" value={address} on:input="{(event)=> address = event.target.value}" />
        <TextInput label ="imageURL" id="imageURL" value={imageUrl} on:input="{(event)=> imageUrl = event.target.value}" />
        <TextInput label ="E-mail" id="email" value={email} on:input="{(event)=> email = event.target.value}" type="email"/>
        
        <TextInput label ="Description" 
        id="description"
        value={description} 
        on:input="{(event)=> description = event.target.value}"
        controlType="textarea"/>
        
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm}>Save</Button>
        
    </div>        
</Modal>