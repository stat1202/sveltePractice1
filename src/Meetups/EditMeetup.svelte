<script>
    import {createEventDispatcher} from "svelte"
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import Modal from "../UI/Modal.svelte";
    import { isEmpty, isValidEmail } from "../helpers/validation"


    let title = ""
    let subtitle = "" 
    let address = ""
    let email ="" 
    let description = "" 
    let imageUrl = ""

    const dispatch = createEventDispatcher()

    $: titleValid = !isEmpty(title)
    $:subtitleValid = !isEmpty(subtitle)
    $:addressValid = !isEmpty(address)
    $:descriptionValid = !isEmpty(description)
    $:imageUrlValid = !isEmpty(imageUrl)
    $: emailValid = isValidEmail(email)
    $: formIsValid = 
    titleValid && 
    subtitleValid && 
    addressValid && 
    descriptionValid && 
    imageUrlValid && 
    emailValid;

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
        <TextInput label ="Title" id="title" value={title} on:input="{(event)=> title = event.target.value}" 
            valid = {titleValid} validityMessage={"Please enter a valid title"}/>
        <TextInput label ="Subitle" id="subtitle" value={subtitle} on:input="{(event)=> subtitle = event.target.value}" 
            valid = {subtitleValid} validityMessage={"Please enter a valid subtitle"}/>
        <TextInput label ="Address" id="address" value={address} on:input="{(event)=> address = event.target.value}" 
            valid = {addressValid} validityMessage={"Please enter a valid address"}/>
        <TextInput label ="imageURL" id="imageURL" value={imageUrl} on:input="{(event)=> imageUrl = event.target.value}" 
            valid ={imageUrlValid} validityMessage={"Please enter a valid imageUrl"}/>
        <TextInput label ="E-mail" id="email" value={email} on:input="{(event)=> email = event.target.value}" type="email"
            valid={emailValid} validityMessage={"Please enter a valid email"}/>
        
        <TextInput label ="Description" 
        id="description"
        value={description} 
        on:input="{(event)=> description = event.target.value}"
        controlType="textarea"
        valid = {descriptionValid}
        validityMessage={"Please enter a valid description"}/>
        
    </form>
    <div slot="footer">
        <Button type="button" mode="outline" on:click={cancel}>Cancel</Button>
        <Button type="button" on:click={submitForm} disabled={!formIsValid}>Save</Button>
        
    </div>        
</Modal>