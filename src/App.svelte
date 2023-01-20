<script>
    import Header from "./UI/Header.svelte"
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import Button from "./UI/Button.svelte";
    import EditMeetup from "./Meetups/EditMeetup.svelte";

    let meetups = [
        {
            id:"m1",
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that teach you how to code!',
            imageUrl : 'http://image.dongascience.com/Photo/2020/03/5bddba7b6574b95d37b6079c199d7101.jpg',
            address: '27th Nerd Roaad, 32523 New York',
            contactEmail: 'code@test.com',
            isFavorite:false
        },
        {
            id:"m2",
            title: 'Swim Together',
            subtitle: 'Let\'s go for some swimming',
            description: 'We will simply swim some rounds!',
            imageUrl : 'http://image.dongascience.com/Photo/2020/03/5bddba7b6574b95d37b6079c199d7101.jpg',
            address: '27th Nerd Roaad, 32523 New York',
            contactEmail: 'swim@test.com',
            isFavorite:false
        }

    ]

    let editMode

    function addMeetup(event){
        
        const newMeetup={
            id: Math.random().toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageUrl: event.detail.imageUrl,
            contactEmail: event.detail.email,
            address: event.detail.address
        };
        meetups = [newMeetup, ...meetups]
        editMode = null
    }

    function toggleFavorite(event) {
        const id = event.detail
        const updatedMeeetup = { ...meetups.find( m=>m.id === id ) }
        updatedMeeetup.isFavorite = !updatedMeeetup.isFavorite
        const meetupIndex = meetups.findIndex( m=> m.id === id)
        const updatedMeetups = [...meetups]
        updatedMeetups[meetupIndex] = updatedMeeetup
        meetups = updatedMeetups
    }

    function cancelEdit(){
        editMode = null
    }
</script>

<style>
    main{
        margin-top: 5rem;
    }

    .meetup-controls{
        margin: 1rem;
    }
</style>

<Header/>
<main>
    <div class="meetup-controls">
        <Button on:click="{()=> editMode = "add"}">
            New Meetup
        </Button>
    </div>
    {#if editMode === 'add'}
        <EditMeetup on:save="{addMeetup}" on:cancel={cancelEdit}/>
    {/if}
    <MeetupGrid {meetups} on:togglefavorite="{toggleFavorite}"/>
</main>

