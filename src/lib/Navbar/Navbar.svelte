<script>
    import { page } from '$app/stores'; 
</script>

<header>
    <nav>
        <ul>
            <li class:active={$page.url.pathname === '/'}>Home</li>
            <li>About</li>
            <li>Search Bar</li>
        </ul>
    </nav>
</header>


<style>
    header{
        background-color: black;
    }
    ul{
        color: orange; 
        padding: 0; 
        margin: 0; 
        display: flex;
        list-style: none;
    }
    li{
        padding: 1rem;
    }
</style>