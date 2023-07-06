<script lang="ts">
    import { onMount } from "svelte";
    import Fa from 'svelte-fa'
    import { faBars, faXmark } from '@fortawesome/free-solid-svg-icons'
    const links = [
        {
            name: 'Home',
            link: '/'
        },
        {
            name: 'About',
            link: '/about'
        },
        {
            name: 'Contact us',
            link: '/contact'
        }
    ];
    let nav, menuOpen = false;
    onMount(() => {
        nav = document.getElementById('navigation');

        // mobileBtn!.addEventListener('click', () => {
        //     mobileMenu!.classList.toggle('inactive');
        // });

        window.addEventListener('resize', () => {
            if (window.innerWidth >= 768) {
                nav!.style.display = 'flex';
            } else {
                nav!.style.display = 'none';
            }
        });
    })
    
</script>

<header class="pr-8">
    <img class="logo" src="/rms-logo.svg" alt="RMS">
    <ul id="navigation">
        {#each links as link}
        <li>
            <a href={link.link}>
                {link.name}
            </a>
        </li>
        {/each}
    </ul>


    <div id="mobileNavigation_btn" role="presentation" class="icon" on:click={() => menuOpen = !menuOpen} on:keypress={() => menuOpen = !menuOpen}>
        <Fa style="pointer-events: none;" icon={menuOpen ? faXmark : faBars} color={menuOpen ? 'black' : 'white'} />
    </div>
    <div id="mobileNavigation_menu" class:active={menuOpen}>
        <ul id="navigation">
            {#each links as link}
            <li>
                <a 
                    href={link.link}>
                    {link.name}
                </a>
            </li>
            {/each}
        </ul>
    </div>
</header>

<style>
    #navigation {
        display: none;
    }
    header {
        position: sticky;
        top: 0;
        z-index: 100;
        width: 100%;
        height: 10vh;
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: #96c3ca;
    }
    li {
        cursor: pointer;
    }
    li:hover {
        color: white;
    }
    a {
        color: black;
        text-decoration: none;
    }
    .logo {
        height: 100%;
    }

    ul#navigation {
        gap: 12vw;
    }

    .icon {
        width: 21px;
        height: 21px;
        color: white;
        
    }
    #mobileNavigation_btn {
        z-index: 10;
    }
    #mobileNavigation_menu {
        height: 0vh;
        transition: height .6s, opacity .32s cubic-bezier(.4,0,.6,1);
        background-color: white;
        color: white;
        font-weight: 700;
        position: fixed;
        top: 0;
        left: 0;
        height: 0;
        width: 100%;
        overflow: hidden;
        opacity: 0;
        padding: 10vh 24px 0 23px;
    }
    #mobileNavigation_menu > ul > li > a {
        color: white;
        line-height: 1rem;
        transition: color .6s ease, line-height .6s ease;
    }
    #mobileNavigation_menu.active > ul > li > a {
        color: black;
        line-height: 4rem;
    }
    #mobileNavigation_menu.active {
        height: 100vh;
        width: 100vw;
        opacity: 1;
    }
    #mobileNavigation_menu #navigation {
        display: block;
    }

    #mobileNavigation_menu a {
        display: block;
        font-size: 2rem;
        line-height: 4rem;
        width: 100%;
    }

    @media (min-width: 768px) {
        #navigation {
            font-size: 1.5rem;
            display: flex;
            
            list-style-type: none;
            padding-right: 5%;
        }
        #mobileNavigation_btn {
            display: none;
            padding-right: 5%;
        }
    }

    @media screen and (min-width: 1024px) { 
        header {
            height: 30vh;
        }
    }
</style>