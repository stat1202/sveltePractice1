<script>
    import Header from "./UI/Header.svelte"
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";

    let title,subtitle, address, email, description, imageURL = ""

    let meetups = [
        {
            id:"m1",
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that teach you how to code!',
            imageUrl : 'http://image.dongascience.com/Photo/2020/03/5bddba7b6574b95d37b6079c199d7101.jpg',
            address: '27th Nerd Roaad, 32523 New York',
            contactEmail: 'code@test.com'
        },
        {
            id:"m2",
            title: 'Swim Together',
            subtitle: 'Let\'s go for some swimming',
            description: 'We will simply swim some rounds!',
            imageUrl : 'http://image.dongascience.com/Photo/2020/03/5bddba7b6574b95d37b6079c199d7101.jpg',
            address: '27th Nerd Roaad, 32523 New York',
            contactEmail: 'swim@test.com'
        }

    ]

    function addMeetup(){
        const newMeetup={
            id: Math.random().toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            imageURL: imageURL,
            contactEmail: email,
            address: address
        }

        meetups = [newMeetup, ...meetups]
    }
</script>

<style>
    main{
        margin-top: 5rem;
    }

    form{
        width:30rem;
        max-width: 90%;
        margin: auto;
    }
</style>

<Header/>
<main>
    <form on:submit|preventDefault="{addMeetup}">
        <TextInput label ="Title" id="title" value={title} on:input="{(event)=> title = event.target.value}" type="text"/>
        <TextInput label ="Subitle" id="subtitle" value={subtitle} on:input="{(event)=> subtitle = event.target.value}" type="text"/>
        <TextInput label ="Address" id="address" value={address} on:input="{(event)=> address = event.target.value}" type="text"/>
        <TextInput label ="imageURL" id="imageURL" value={imageURL} on:input="{(event)=> imageURL = event.target.value}" type="text"/>
        <TextInput label ="E-mail" id="email" value={imageURL} on:input="{(event)=> email = event.target.value}" type="email"/>

        <TextInput label ="Description" 
        id="description"
        value={description} 
        on:input="{(event)=> description = event.target.value}"
        controlType="textarea"/>
        <Button type="submit" caption="Save" />
        
    </form>
    <MeetupGrid {meetups}/>
</main>

