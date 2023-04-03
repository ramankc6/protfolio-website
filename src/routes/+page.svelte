


<script lang="js">
//-------Imports-------//

//Import onMount (runs when the website loads)
import { onMount } from "svelte";
import { fade } from 'svelte/transition';
import { fly } from 'svelte/transition';


//-------Variable declarations-------//

//Index Declarations
let textIndex = 0;
let fullTextIndex = 0;
let cursorIndex = 0;
let mouseAnnimationIndex = 1;
let scaleIndex = 1;

//Changing Text Declaration
let text = "";
let cursorColor = "#aeafad";


//Const Text Declaration
const fullText = ["Hey Snap!", "My name is Raman Khatri Chhetri"];
const lessThan = '<';
const greaterThan = '>';
let laptopSize;
let resumeTrans;
let experinceTrans;
let contactTrans;
let projectsTrans;

//Scrolling Declaration
let y = 0;
let scale = 1;
let userWidth;
let laptopImg = '/laptop.png';
let scrollImg = '/mouseScroll.png';

//Boolean Declarations
let resume = true
let experince = true
let contact = true
let projects = true
let showScroller = false


//-------Start onMount-------//

//When the user loads the website it calls cusor Annimation which starts the typing annimation
onMount(async () => {
    cursorAnnimation();
    imageResizer();
    updateOptionsDiv();
});

//-------Functions-------//

//Scrolling Funtion

//Cursor Function that blinks the cursor and then calls the typer and deleter depending on if the text is apearing or not
function cursorAnnimation() {
    if (cursorIndex !== 5) {
        cursorColor = cursorIndex % 2 === 0 ? "#aeafad" : "#1e1e1e";
        cursorIndex++;
        setTimeout(cursorAnnimation, 500);
    } else {
        if (textIndex != 0) {
            setTimeout(deleter, 250);
        } else {
            setTimeout(writer, 250);
        }
    }
}

//Function that writes the text, goes back to cursor when done
function writer() {
    if (textIndex < fullText[fullTextIndex].length + 1) {
        text += fullText[fullTextIndex].charAt(textIndex);
        textIndex++;
        setTimeout(writer, 100);
    } else {
        if (fullTextIndex < fullText.length - 1) {
            cursorIndex = 0;
            cursorColor = "#1e1e1e";
            setTimeout(cursorAnnimation, 500);
        } else {
            cursorColor = "#1e1e1e";
            setTimeout(mouseAnnimation, 300)
        }
    }
}

function mouseAnnimation() {
    if (mouseAnnimationIndex % 2 == 0) {
        showScroller = false
        mouseAnnimationIndex++
        setTimeout(mouseAnnimation, 600)
    } else{
        showScroller = true
        mouseAnnimationIndex++
        setTimeout(mouseAnnimation, 1000)
    }
}

//Fnction that deletes the text, goes back to cursor when done
function deleter() {
    if (textIndex !== 0) {
        text = text.substr(0, textIndex - 1);
        textIndex--;
        setTimeout(deleter, 50);
    } else {
        if (fullTextIndex < fullText.length - 1) {
            fullTextIndex++;
            cursorIndex = 0;
            cursorColor = "#1e1e1e";
            setTimeout(cursorAnnimation, 500);
        }
    }
}

function imageResizer() {
    if (userWidth <= 767) {
        laptopImg = '/phone.png'
        scrollImg = '/mobileScroll.png'
    }
    if (y > 900 && y < 1300) {
        scale = 1 + (y - 900) / 1000;
        laptopSize.style.transform = `scale(${scale})`;
        setTimeout(imageResizer, 0)
    }else {
        setTimeout(imageResizer, 0)
    }
}

function buttonPressed (buttonType) {
    if (buttonType == 'resume') {
        contact = false;
        projects = false;
        experince = false;
        resumeTrans.style.transform = `scale(${scaleIndex * 3})`;
        experinceTrans.style.transform = `scale(${0})`;
        contactTrans.style.transform = `scale(${0})`;
        projectsTrans.style.transform = `scale(${0})`;
    } else if (buttonType == 'contact') {
        resume = false;
        projects = false;
        experince = false;
        contactTrans.style.transform = `scale(${scaleIndex * 3})`;
        experinceTrans.style.transform = `scale(${0})`;
        projectsTrans.style.transform = `scale(${0})`;
        resumeTrans.style.transform = `scale(${0})`;
    } else if (buttonType == 'projects') {
        contact = false;
        resume = false;
        experince = false;
        projectsTrans.style.transform = `scale(${scaleIndex * 3})`;
        experinceTrans.style.transform = `scale(${0})`;
        contactTrans.style.transform = `scale(${0})`;
        resumeTrans.style.transform = `scale(${0})`;
    } else if (buttonType == 'experince') {
        contact = false;
        projects = false;
        resume = false;
        experinceTrans.style.transform = `scale(${scaleIndex * 3})`;
        projectsTrans.style.transform = `scale(${0})`;
        contactTrans.style.transform = `scale(${0})`;
        resumeTrans.style.transform = `scale(${0})`;
    }
}

function updateOptionsDiv() {
    if (y <= 1400) {
        resume = true;
        projects = true;
        experince = true;
        contact = true;

    }
    setTimeout(updateOptionsDiv, 0)
}
</script>



<style>

@import url('https://fonts.cdnfonts.com/css/cascadia-code');

body{
    background-color: #1e1e1e;
    min-height: 10000px;
    margin: 0;
}

#cursor {
    transition: color 0.3s;
}

.inequalitySymbols {
    color: #808080;
}

.letterP {
    color: #569cd6;
}

.typingText {
    color: #cecece;
}

.introText{
    font-family: 'Cascadia Code', sans-serif;
    text-align: center;
    font-size: 2vw;
}

.typingDiv {
    min-width: 50vw;
}
.introContainer{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: fixed;
}

.introPage {
    min-height: 100vh;
    min-width: 100vw;
    display: flex;
    justify-content: center;
    z-index: 1;
}
.aboutPage {
    min-height: 100vh;
    min-width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
}
.headshotDiv {
    display: flex;
    height: 68vh;
    align-items: flex-end;
}

.headshotImg {
    min-height: 56vh;
    min-width: 31.25vw;
}


.aboutBackground {
    position: fixed;
    z-index: 2;
    width: 100%;
    height: 100%;
    overflow-x: hidden;
    overflow-y: hidden;
}

.laptopImg {
    width: 100%;
    height: 100%;
    transition: transform 0.1s ease;
}

.aboutContainer {
    z-index: 3;
    position: fixed;
    font-family: 'Cascadia Code', sans-serif;
    text-align: center;
    font-size: 2vw;
    color:white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;
    position: fixed;
    /* top: 20%; */
}

.aboutTextDiv{
    width: 50%;
}

.optionsDiv {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    align-content: center;
    overflow-x: hidden;
    overflow-y: hidden;
}

.leftOptionsDiv,
.rightOptionsDiv {
    display: flex;
    flex-direction: column;
    width:100%;
    height: 100%;
}

.resumeDiv,
.projectsDiv,
.experinceDiv,
.contactDiv {
    height: 100%;
    width: 100%;
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    transition: transform 1.5s;
    /* border: 0; */
}
.resumeDiv:hover,
.projectsDiv:hover,
.experinceDiv:hover,
.contactDiv:hover {
    transition: 0.5s;
    height: 120%;
    width: 140%;
}
.titleText {
    color:white;
    font-size: 45px;
    margin-top: 10%;
}

.optionsIcon {
    height: 25%;
    width: 25%;

}

button{
    border-radius: 0px;
    padding: 0px;
}

.scrollerContainer {
    z-index: 5;
    position: fixed;
    display: flex;
    min-width: 50vw;
    justify-content: center;
}


.mouseImg {
    z-index: 5;
    position: fixed;
    height: 8vh;
    width: 8w;

}
</style>

<body>
    {#if y > 50 && y < 1300}
        <div class= 'aboutBackground' in:fade><img bind:this="{laptopSize}" src = {laptopImg} alt = 'laptop' class = 'laptopImg' style= 'transform: {1 + (y - 50) / 1000}'></div>
    {:else if y < 50}
        <div class = 'introPage'>
            <div class = 'introContainer'>
                <div class = 'headshotDiv'>
                    <img src= {'/headshot.png'} alt='headshot' class='headshotImg'>
                </div>
                <div class= 'typingDiv'>
                    <p class= "introText" >
                        <span class="inequalitySymbols">{lessThan}</span><span class='letterP'>
                        p</span><span class="inequalitySymbols">
                        {greaterThan}</span><span class=typingText>
                        {text}</span><span id="cursor" style="color: {cursorColor};">
                        |</span><span class="inequalitySymbols">
                        {lessThan}/</span><span class='letterP'>
                        p</span><span class="inequalitySymbols">
                        {greaterThan}</span>
                    </p>
                    {#if showScroller == true}
                        <div class='scrollerContainer' in:fade out:fly="{{y: 40, duration: 1000}}">
                            <img src= {scrollImg} alt='mouseScroll' class = 'mouseImg'>
                        </div>
                    {/if}
                </div>
            </div>
        </div>
    {/if}
    {#if y > 50 && y < 1100}
        <div class='aboutPage'>
            <div class='aboutContainer' in:fade>
                <div>
                    <p>About</p>
                </div>
                <div class='aboutTextDiv'>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Commodi voluptas, quo repellendus doloremque fuga reprehenderit incidunt quaerat saepe laboriosam, expedita tempora neque ad quisquam quam perferendis vel autem magnam hic?</p>
                </div>
            </div>
        </div>
    {/if}
    {#if y > 1400}
        <div class='optionsDiv'>
            <div class='leftOptionsDiv'>
                {#if resume == true}
                    <button bind:this="{resumeTrans}" on:click = {() => buttonPressed('resume')} class='resumeDiv' style='background-color: red' transition:fly={{ x: -100, y: -100, duration: 1000 }}>
                    {#if projects == true}
                        <p class='titleText'>Reusme</p>
                        <img src='/placeholder.jpeg' alt='resumeIcon' class='optionsIcon'>
                    {/if}
                    </button>
                {/if}
                {#if projects == true}
                    <button bind:this="{projectsTrans}" on:click = {() => buttonPressed('projects')} class='projectsDiv' style='background-color: green;' transition:fly={{ x: -100, y: 100, duration: 1000 }}>
                    {#if resume == true}
                        <p class='titleText'>Projects</p>
                        <img src='/placeholder.jpeg' alt='projectsIcon' class='optionsIcon'>
                    {/if}
                    </button>
                {/if}
            </div>

            <div class='rightOptionsDiv'>
                {#if experince == true}
                    <button bind:this="{experinceTrans}" on:click = {() => buttonPressed('experince')} class='experinceDiv' style='background-color: yellow;' transition:fly={{ x: 100, y: -100, duration: 1000 }}>
                        {#if projects == true}
                            <p class='titleText'>Experince</p>
                            <img src='/placeholder.jpeg' alt='experinceIcon' class='optionsIcon'>
                        {/if}
                    </button>
                {/if}
                {#if contact == true}
                    <button bind:this="{contactTrans}" on:click = {() => buttonPressed('contact')} class='contactDiv' style='background-color: blue;' transition:fly={{ x: 100, y: 100, duration: 1000 }}>
                    {#if projects == true}
                        <p class='titleText'>Contact</p>
                        <img src='/placeholder.jpeg' alt='contactIcon' class='optionsIcon'>
                    {/if}
                    </button>
                {/if}
            </div>
        </div>
    {/if}
</body>

<svelte:window bind:scrollY={y} bind:innerWidth={userWidth} />