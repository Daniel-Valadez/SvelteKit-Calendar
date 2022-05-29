<script>

    import { onMount } from 'svelte'; //Need to use this in order to reference 'document'
    
    //Going to be creating a dynamic way of getting dates to populate the calendar. 
    const date = new Date();

    //getMonth will give us a number. Can use that number to access
    //the proper month in an object of months. 
    const months = [
        "January",
        "February",
        "March", 
        "April", 
        "May", 
        "June", 
        "July", 
        "August", 
        "September", 
        "Ocotber", 
        "November", 
        "December"
    ]

    let days = ""

    onMount(() => {
        document.querySelector('.current-date h1').innerHTML = months[date.getMonth()]; 
        document.querySelector('.current-date p').innerHTML = date.toDateString();
        /*for(let i = 1; i <= 31; ++i){
            days += `<`
        }*/
    }); 
    //document.querySelector('.current-date h1').innerHTML = months[date.getMonth()]; 
    //document.querySelector('.current-date p').innerHTML = date.toDateString(); 
</script>

<section class="container">
    <div class="calendar">
        <div class="month">
            <span class="left arrow"></span>
            <div class="current-date">
                <h1>Month</h1>
                <p>Today's Date</p>
            </div>
            <span class="right arrow"></span>
        </div>
        <div class="days">
            <div>Sun</div>
            <div>Mon</div>
            <div>Tue</div>
            <div>Wed</div>
            <div>Thur</div>
            <div>Fri</div>
            <div>Sat</div>
            <div class="days-inner">1, 2, 3...31</div>
        </div>
    </div>
</section>

<style>
    .month{
        max-width: 100%;
        height: 12rem;
        background-color: orange;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 2rem; 
        text-align: center;
        text-shadow: 0 0.3rem .5rem rgba(0, 0, 0, 0.5);
    }
    .month h1{
        font-size: 3rem;
        font-weight: normal;
        text-transform: uppercase;
        letter-spacing: 0.2rem;
        margin-bottom: 1rem;
    }
    
    .month p {
        font-size: 1.6rem;
    }
    .days{
        width: 100%;
        height: 5rem;
        padding: 0 0.4rem; 
        display: flex;
        align-items: center;
    }
    .days div{
        font-size: 1.5rem;
        font-weight: lighter;
        letter-spacing: 0.1rem;
        width: calc(44.2rem / 7) ;
        display: flex;
        justify-content: center;
        align-items: center;
        text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
    }
    .days-inner{
        width: 100%;
        display: flex;
        flex-wrap:wrap;
        padding: 0.2rem;
    }
</style>