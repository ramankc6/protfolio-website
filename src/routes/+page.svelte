


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

//Changing Text Declaration
let text = "";
let cursorColor = "#aeafad";


//Const Text Declaration
const fullText = ["Hey Snap!", "My name is Raman Khatri Chhetri"];
const lessThan = '<';
const greaterThan = '>';
let laptopImage;
let resumeTrans;
let experinceTrans;
let contactTrans;
let projectsTrans;

//Scrolling Declaration
let y = 0;
let scale = 1;

//Boolean Declarations
let resume = true
let experince = true
let contact = true
let projects = true


//-------Start onMount-------//

//When the user loads the website it calls cusor Annimation which starts the typing annimation
onMount(async () => {
    cursorAnnimation();
    imageResizer();
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
        }
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
    if (y > 500 && y < 900) {
        scale = 1 + (y - 500) / 1000;
        laptopImage.style.transform = `scale(${scale})`;
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
        resumeTrans.style.transform = `scale(${3})`;
    } else if (buttonType == 'contact') {
        resume = false;
        projects = false;
        experince = false;
        contactTrans.style.transform = `scale(${3})`;
    } else if (buttonType == 'projects') {
        contact = false;
        resume = false;
        experince = false;
        projectsTrans.style.transform = `scale(${3})`;
    } else if (buttonType == 'experince') {
        contact = false;
        projects = false;
        resume = false;
        experinceTrans.style.transform = `scale(${3})`;
    }
}

</script>



<style>

@import url('https://fonts.cdnfonts.com/css/cascadia-code');

body{
    background-color: #1e1e1e;
    min-height: 100000px;
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
    font-size: 30px;
}

.introContainer{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;
    position: fixed;
    left: 25%
}

.headshotDiv {
    display: flex;
    height: 68vh;
    align-items: flex-end;
}

.headshotImg {
    min-height: 56vh;
    min-width: 56.5vh;
}


.introBackground {
    position: fixed;
    z-index: 1;
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
    font-size: 30px;
    color:white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;
    position: fixed;
    top: 20%;
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
    transition: 1.5s;
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


</style>

<body>
    {#if y > 50 && y < 900}
    <div class= 'introBackground' transition:fade><img bind:this="{laptopImage}" src = '/laptop.png' alt = 'laptop' class = 'laptopImg' style= 'transform: {1 + (y - 50) / 1000}'></div>
    {:else if y < 50}
    <div class = 'introContainer' transition:fade>
        <div class = 'headshotDiv'><img src= '/headshot.png' alt='headshot' class='headshotImg'></div>
        <div>
            <p class= "introText">
                <span class="inequalitySymbols">{lessThan}</span><span class='letterP'>
                p</span><span class="inequalitySymbols">
                {greaterThan}</span><span class=typingText>
                {text}</span><span id="cursor" style="color: {cursorColor};">
                |</span><span class="inequalitySymbols">
                {lessThan}/</span><span class='letterP'>
                p</span><span class="inequalitySymbols">
                {greaterThan}</span>
            </p>
        </div>
    </div>
    {/if}
    {#if y > 50 && y < 600}
        <div class='aboutContainer' transition:fade>
            <div>
                <p>About</p>
            </div>
            <div class='aboutTextDiv'>
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Commodi voluptas, quo repellendus doloremque fuga reprehenderit incidunt quaerat saepe laboriosam, expedita tempora neque ad quisquam quam perferendis vel autem magnam hic?</p>
            </div>
        </div>
    {/if}
    {#if y > 1100}
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

<svelte:window bind:scrollY={y} />