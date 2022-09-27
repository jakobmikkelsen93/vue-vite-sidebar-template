<script setup>
import { ref } from 'vue';
import { useCounterStore } from '../stores/counter'
const userStore = useCounterStore()


const body = document.querySelector('body')
const sidebar = body.querySelector('nav')
const toggled = body.querySelector(".toggle")
const searchBtn = body.querySelector(".search-box")
const toggleSwitch = document.querySelector('#theme-switch input[type="checkbox"]');

let active = false
let search = ref('')
const userTheme = "light-theme"
// const modeSwitch = body.querySelector(".toggle-switch")

//function that changes the theme, and sets a localStorage variable to track the theme between page loads
function switchTheme(e) {
    if (e.target.checked) {
        localStorage.setItem('theme', 'dark');
        document.documentElement.setAttribute('data-theme', 'dark');
        toggleSwitch.checked = true;
    } else {
        localStorage.setItem('theme', 'light');
        document.documentElement.setAttribute('data-theme', 'light');
        toggleSwitch.checked = false;
    }    
}

//listener for changing themes
// toggleSwitch.addEventListener('change', switchTheme, false);

// //pre-check the dark-theme checkbox if dark-theme is set
// if (document.documentElement.getAttribute("data-theme") == "dark"){
//     toggleSwitch.checked = true;
// }

const detectColorScheme = () => {
    var theme="light";    //default to light

    //local storage is used to override OS theme settings
    if(localStorage.getItem("theme")){
        if(localStorage.getItem("theme") == "dark"){
            var theme = "dark";
        }
    } else if(!window.matchMedia) {
        //matchMedia method not supported
        return false;
    } else if(window.matchMedia("(prefers-color-scheme: dark)").matches) {
        //OS theme setting detected as dark
        var theme = "dark";
    }

    //dark theme preferred, set document with a `data-theme` attribute
    if (theme=="dark") {
         document.documentElement.setAttribute("data-theme", "dark");
    }
    console.log(theme)
}

const ToggleMenu = () => {
    console.log('toggling')
    const sidebar = document.querySelector("body > nav")
    if (sidebar.classList.contains('close')){
        sidebar.classList.remove('close')
    }
    else {
        sidebar.classList.add('close')
    }
}

const openMenu = () => {
    if(active === false) {
        console.log('toggling')
        const sidebar = document.querySelector("body > nav")
        sidebar.classList.remove('close')}
    active = true
}
const deToggleMenu = () => {
    if(active === true) {
        console.log('toggling')
        const sidebar = document.querySelector("body > nav")
        sidebar.classList.add('close') 
    }
    active = false
}

const ToggleSearch = () => {
    const sidebar = document.querySelector("body > nav")
    if (sidebar.classList.contains('close')){
        sidebar.classList.remove('close')
    }
    const searchField = document.querySelector("body > nav > div > div.menu > li > input[type=text]")
    searchField.focus()
    search = ''
}

const modeSwitch = () => {
    body.classList.toggle("dark");
    const modeText = body.querySelector(".mode-text");
    const modeSwitch = body.querySelector(".toggle-switch")    
    if(body.classList.contains("dark")){
        modeText.innerText = "Light mode";
    }else{
        modeText.innerText = "Dark mode";
    }
}


</script>



<template>

<aside>
<body>
    <nav @mouseover="openMenu" @mouseleave="deToggleMenu" class="sidebar close">
        <header>
            <div class="image-text">
                <span class="image">
                    <img src="../assets/logo.svg" alt="">
                </span>

                <div class="text logo-text">
                    <span class="name">Justitsministeriet</span>
                    <span class="profession"> Human Resource</span>
                </div>
            </div>

            <i @click="ToggleMenu" class='bx bx-chevron-right toggle'></i>
        </header>

        <div class="menu-bar">
            <div class="menu">

                <li class="search-box">
                    <i @click="ToggleSearch" class='bx bx-search icon'></i>
                    <input type="text" v-model="search" placeholder="search...">
                </li>

                <ul class="menu-links">
                    <li class="nav-link">
                        <a @click="detectColorScheme" href="#">
                            <i class='bx bx-home-alt icon' ></i>
                            <span class="text nav-text">Dashboard</span>
                        </a>
                    </li>

                    <li class="nav-link">
                        <a href="#">
                            <i class='bx bx-bar-chart-alt-2 icon' ></i>
                            <span class="text nav-text">Revenue</span>
                        </a>
                    </li>

                    <li class="nav-link">
                        <a href="#">
                            <i class='bx bx-bell icon'></i>
                            <span class="text nav-text">Notifications</span>
                        </a>
                    </li>

                    <li class="nav-link">
                        <a href="#">
                            <i class='bx bx-pie-chart-alt icon' ></i>
                            <span class="text nav-text">Analytics</span>
                        </a>
                    </li>

                    <li class="nav-link">
                        <a href="#">
                            <i class='bx bx-heart icon' ></i>
                            <span class="text nav-text">Likes</span>
                        </a>
                    </li>

                    <li class="nav-link">
                        <a href="#">
                            <i class='bx bx-wallet icon' ></i>
                            <span class="text nav-text">Wallets</span>
                        </a>
                    </li>

                </ul>
            </div>

            <div class="bottom-content">
                <li class="">
                    <a href="#">
                        <i class='bx bx-log-out icon' ></i>
                        <span class="text nav-text">Logout</span>
                    </a>
                </li>

                <li class="mode">
                    <div class="sun-moon">
                        <i class='bx bx-moon icon moon'></i>
                        <i class='bx bx-sun icon sun'></i>
                    </div>
                    <span class="mode-text text">Dark mode</span>

                    <div @click="modeSwitch" class="toggle-switch">
                        <span class="switch"></span>
                    </div>
                </li>
                
            </div>
        </div>
    </nav>
</body>

</aside>


</template>

