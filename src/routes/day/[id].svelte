<!--The brackets over the name will allow this page to
pool dynamic data.-->
<script>
    //Need to parse the URL to find out what the day is.  
    import { page } from '$app/stores'; 
    const date = $page.url.pathname.replace('/day/', '');
    //console.log(day);
</script> 

<h2>{date}</h2>


<style>
    h2{
        font-size: 2rem;
    }
</style>