
<script lang="js">
//-------Imports-------//

//Import onMount (runs when the website loads)
import { onMount } from "svelte";
import { fade } from 'svelte/transition';
import { fly } from 'svelte/transition';
import { slide } from 'svelte/transition';

//-------Variable declarations-------//

//Index Declarations
let textIndex = 0;
let fullTextIndex = 0;
let cursorIndex = 0;
let mouseAnnimationIndex = 1;
let scaleIndex = 1;
let daysProgStart = 0;
let daysProgEnd = 0;
let gradYear = 2000;
let numRepos = 0;
let gpa = 0.0;

//Changing Text Declaration
let text = "";
let cursorColor = "#aeafad";
let toolsHover = '';

//Const Text Declaration
const fullText = ["Hey Snap!", "My name is Raman Khatri Chhetri"];
const lessThan = '<';
const greaterThan = '>';

//Undefined Declarations
let laptopSize;
let resumeTrans;
let skillsTrans;
let contactTrans;
let projectsTrans;
let userWidth;
let audio;
let hoverTitle;
let body;

//Scrolling Declaration
let y = 0;
let scale = 1;

//Image Chnage Declaration
let laptopImg = '/laptop.png';
let scrollImg = '/mouseScroll.png';

//Boolean Declarations
let resume = true
let skills = true
let contact = true
let projects = true
let showScroller = false
let resumePage = false
let skillsPage = false
let now = new Date(), month, day, year;
let contactPage = false
//-------Start onMount-------//

//When the user loads the website it calls cusor Annimation which starts the typing annimation
onMount(async () => {
    // alert('This website is still under construction, please excuse the mess')
    cursorAnnimation();
    imageResizer();
    updateOptionsDiv();
    // drake();
    // y = 0;
    findDate();

});

//-------Functions-------//

function findDate() {
    month = (now.getMonth());
    day = now.getDate();
    year = now.getFullYear();
    daysProgEnd = (Math.floor((month * 30.437) + day + ((year - 2020) * 365.25))) - 817;
}

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
    else {
        laptopImg = '/laptop.png'
        scrollImg = '/mouseScroll.png'
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
        skills = false;
        resumeTrans.style.transform = `scale(${scaleIndex * 3})`;
        skillsTrans.style.transform = `scale(${0})`;
        contactTrans.style.transform = `scale(${0})`;
        projectsTrans.style.transform = `scale(${0})`;
        resumePage = true;
        
    } else if (buttonType == 'contact') {
        resume = false;
        projects = false;
        skills = false;
        contactTrans.style.transform = `scale(${scaleIndex * 3})`;
        skillsTrans.style.transform = `scale(${0})`;
        projectsTrans.style.transform = `scale(${0})`;
        resumeTrans.style.transform = `scale(${0})`;
        contactPage = true;
    } else if (buttonType == 'projects') {
        contact = false;
        resume = false;
        skills = false;
        projectsTrans.style.transform = `scale(${scaleIndex * 3})`;
        skillsTrans.style.transform = `scale(${0})`;
        contactTrans.style.transform = `scale(${0})`;
        resumeTrans.style.transform = `scale(${0})`;
    } else if (buttonType == 'skills') {
        contact = false;
        projects = false;
        resume = false;
        skillsTrans.style.transform = `scale(${scaleIndex * 3})`;
        projectsTrans.style.transform = `scale(${0})`;
        contactTrans.style.transform = `scale(${0})`;
        resumeTrans.style.transform = `scale(${0})`;
        skillsPage = true;
        dayProgAnimation();
        gradYearAnimation();
        reposAnimation();
        gpaAnimation();
    }
}

function dayProgAnimation() {
    if (daysProgStart < daysProgEnd) {
        daysProgStart += 1;
        setTimeout(dayProgAnimation, 0.02*daysProgStart)
    }
}

function gradYearAnimation() {
    if (gradYear < 2026) {
        gradYear += 1;
        setTimeout(gradYearAnimation, 0.06*gradYear)
    }
}

function reposAnimation() {
    if (numRepos < 16) {
        numRepos += 1;
        setTimeout(reposAnimation, 20*numRepos)
    }
}

function gpaAnimation() {
    if (gpa < 4.0) {
        gpa += 0.01;
        setTimeout(gpaAnimation, 0.1*gpa)
    }
}

// function drake() {
//     audio.play();
//     setTimeout(drake, 100)
// }

function updateOptionsDiv() {
    if (y <= 1400) {
        resume = true;
        projects = true;
        skills = true;
        contact = true;
        resumePage = false;
        skillsPage = false;
        daysProgStart = 0;
        gradYear = 2000;
        numRepos = 0;
        gpa = 0;
        contactPage = false;

    }
    setTimeout(updateOptionsDiv, 0)
}

function mouseOverLogo(logoType) {
    if (logoType == 'aws') {
        toolsHover = 'AWS'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'colab') {
        toolsHover = 'Google Colab'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'figma') {
        toolsHover = 'Figma'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'flutter') {
        toolsHover = 'Flutter'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'git') {
        toolsHover = 'Git'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'react') {
        toolsHover = 'React'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'svelte') {
        toolsHover = 'Svelte'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'tensorflow') {
        toolsHover = 'Tensorflow'
        hoverTitle.style.opacity = 1
    }
    else if (logoType == 'none') {
        hoverTitle.style.opacity = 0
    }
}

</script>



<style>

@import url('https://fonts.cdnfonts.com/css/cascadia-code');
@import url('https://fonts.googleapis.com/css2?family=Palanquin+Dark&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro&display=swap');

body{
    background-color: #1e1e1e;
    min-height: 10000px;
    margin: 0;
    background-size: 110%;
    background-position: 4% 4%;
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
    display: flex;
    justify-content: center;
    align-items: center;
}

.laptopImg {
    width: 85%;
    height: 85%;
}

.aboutContainer {
    z-index: 3;
    position: fixed;
    font-family: 'Source Code Pro', monospace;
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
    width: 95%;
    height: 95%;
    position: fixed;

    align-content: center;
    /* overflow-x: hidden;
    overflow-y: hidden; */
}

.leftOptionsDiv,
.rightOptionsDiv {
    display: flex;
    flex-direction: column;
    width:100%;
    height: 100%;

}

.leftOptionsDiv {
    margin-right: 5%;
}

.resumeDiv,
.projectsDiv,
.skillsDiv,
.contactDiv {
    height: 100%;
    width: 100%;

    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: 1s;
    margin: 2%;
    border-radius: 4%;
    background-size: 110%;
    background-position: 4% 4%;
    border: 0;
}

.contactDiv,
.skillsDiv {
    justify-content: left;
    align-items: left;
}

.resumeDiv,
.projectsDiv {
    align-items: center;
}

.resumeDiv:hover,
.projectsDiv:hover,
.skillsDiv:hover,
.contactDiv:hover {
    transition: 0.5s;
    height: 105%;
    width: 105%;
}
.titleText {
    font-size: 40px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
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

.optionsPage {
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;

}

.resumeTitle {
    color: white;
    background-color: #1e1e1e;
    border-radius:40px/55%;
    min-width: 30%;
    text-align: center;
    color:white;
    font-size: 40px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
}
.projectsTitle {
    min-width: 30%;
    text-align: center;
    color:white;
    font-size: 40px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
}
.contactTitle,
.skillsTitle{
    color: black;
    min-width: 30%;
    text-align: center;
    font-size: 40px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
}

/* audio{
    opacity: 0;
} */

.rightOptionsDiv { direction: rtl; }
.rightOptionsDiv > * { direction: ltr; }

.resumePageContainer {
    z-index: 7;
    display: flex;
    position: fixed;
    width: 100%;
    height: 100%;
    justify-content: center;
    align-items: center;
}

.resumePageDiv {
    width: 80%;
    height: 100%;
}

.resumePdf {
    width: 100%;
    height: 100%;
}

/* Skills Page */

.skillsPageContainer {
    z-index: 7;
    display: flex;
    position: fixed;
    width: 90%;
    height: 100%;
    flex-direction: column;
    justify-content: top;
    align-items: center;
    left:5%;
}

.skillsTitleDiv {
    text-align: center;
}

.skillsTitleText {
    font-size: 30px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
}

.langDiv {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 50%;
    border-bottom: 2px solid white;
    padding-bottom: 1%;
}

.frontEndDiv {
    display: flex;
    flex-direction: column;
    width: 30%;
    border-right: 2px solid white;
    align-items: center;
}

.toolsDiv {
    display: flex;
    flex-direction: column;
    width: 40%;
    align-items: center;
}
.backEndDiv {
    display: flex;
    flex-direction: column;
    border-left: 2px solid white;
    width: 30%;
    align-items: center;
}

.infoDiv {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 35%;
    padding-top: 1%;
}
.daysProgDiv,
.gradYearDiv,
.reposDiv,
.gpaDiv {
    width: 25%;
    display: flex;
    flex-direction: column;
    justify-content: start;
}

.gradYearDiv {
    border-left: 2px solid white;
    border-right: 2px solid white;
}

.reposDiv {
    border-right: 2px solid white;

}

.frontEndTitle,
.backEndTitle,
.toolsTitle {
    font-size: 20px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
}

.langContainer {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100%;
    justify-content: center;
    align-items: center;
    justify-content: space-evenly;
}

.langBoxes {
    display: flex;
    flex-direction: row;
    width: 75%;
    background-color: red;
    border-radius:20px/50%;
    margin: 0%;
    transition: 0.5s;
}

.langText {
    font-size: 20px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    width: 100%;
    text-align: center;
}

.langBoxes:hover {
    width: 83%;
    transition: 0.5s;
}

.toolsLogoContainer {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 80%;
    align-items: center;
    justify-content: space-evenly;
}

.toolsRow {
    display: flex;
    flex-direction: row;
    width: 100%;
    height: 25%;
    align-items: center;
    justify-content: space-evenly;
}

.toolsLogoImg {
    width: 15%;
    height: 80%;
}
.infoNum {
    font-size: 100px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    width: 75%;
    height: 60%;
    text-align: center;
    margin-bottom: 8%;
    border-bottom: blue 10px solid;
    align-self: center;
    padding-bottom: 5%;
    transform: scale(1);
    transition: 0.5s;
}

.infoNum:hover {
    transform: scale(1.1);
    transition: 0.5s;
}
.infoTitle {
    margin-left: 4%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    width: 100%;
    height: 40%;
    text-align: center;
}

.infoText {
    font-size: 100%;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    width: 100%;
    height: 100%;
    text-align: left;
    margin: 0%;
}

.hoverTitle {
    font-size: 40px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    transition: 0.5s;
}

.contactPageContainer {
    z-index: 9;
    display: flex;
    position: fixed;
    width: 100%;
    height: 100%;
    left: 7.3%;
    /* right: 5.1%; */
    /* bottom: 5vh;
    top: 0.5vh; */
}
.contactBox {
    background-image: url('contactBackground.png');
    background-size: 100%;
    background-position: 4% 4%;
    background-repeat: no-repeat;
    width: 85%;
    height: 95%;
    display: flex;
    flex-direction: row;
    justify-content: right;


}
.contactLogoImg {
    background:none;
    width: 100%;
    height: 100%;
}
.contactButton {
    background: none;
    border: none;
    height:10%;
    margin-top: 60%;
}
.contactRow {
    display: flex;
    flex-direction: column;
    width: 10%;
    height: 100%;
    align-items: flex-start;
    justify-content: flex-start;
    margin-right: 5%;
}
.contactPageTitle {
    padding-right: 34%;
}

.contactButton:hover {
    transform: scale(0.9);
    transition: 0.5s;
}

@media only screen and (max-width: 767px) {
    .laptopImg{
        max-height: 70%;
    }
    .langText {
        font-size: 15px;
    }
    .infoNum {
        font-size: 25px;
    }
    .infoTitle,
    .infoText {
        font-size: 10px;
    }
}   
</style>

<body>
    <!-- <audio controls autoplay bind:this={audio}>
        <source src='/music.mp3' type='audio/mp3'>
    </audio> -->
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
                        h1</span><span class="inequalitySymbols">
                        {greaterThan}</span><span class=typingText>
                        {text}</span><span id="cursor" style="color: {cursorColor};">
                        |</span><span class="inequalitySymbols">
                        {lessThan}/</span><span class='letterP'>
                        h1</span><span class="inequalitySymbols">
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
                    <p>
                        <span class="inequalitySymbols">{lessThan}</span><span class='letterP'>
                            h2</span><span class="inequalitySymbols">
                            {greaterThan}</span><span class=typingText>
                            About</span><span class="inequalitySymbols">
                            {lessThan}/</span><span class='letterP'>
                            h2</span><span class="inequalitySymbols">
                            {greaterThan}</span>
                    </p>
                </div>
                <div class='aboutTextDiv'>
                    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Commodi voluptas, quo repellendus doloremque fuga reprehenderit incidunt quaerat saepe laboriosam, expedita tempora neque ad quisquam quam perferendis vel autem magnam hic?</p>
                </div>
            </div>
        </div>
    {/if}
    {#if y > 1400}
        <div class ='optionsPage'>
            <div class='optionsDiv'>
                <div class='leftOptionsDiv'>
                    {#if resume == true && resumePage == false}
                        <button bind:this="{resumeTrans}" on:click = {() => buttonPressed('resume')} class='resumeDiv' style='background-image: url("/resumeBackground.png");' in:fly={{ x: -100, y: -100, duration: 1000 }} out:fade>
                        {#if projects == true}
                            <div class='resumeTitle'>
                            <p class='titleText'>Resume</p>
                            </div>
                            <!-- <img src='/resumeIcon.png' alt='resumeIcon' class='optionsIcon'> -->
                        {/if}
                        </button>
                    {/if}
                    {#if resumePage == true}
                    <div transition:fade class='resumePageContainer'>
                        <div class= 'resumePageDiv'>
                            <iframe class = 'resumePdf' title='' src="/Resume.pdf#toolbar=0" width="100%" height="500px">
                            </iframe>
                        </div>
                    </div>
                    {/if}
                    {#if projects == true}
                        <button bind:this="{projectsTrans}" on:click = {() => buttonPressed('projects')} class='projectsDiv' style='background-image: url("/projectBackground.png");' transition:fly={{ x: -100, y: 100, duration: 1000 }}>
                        {#if resume == true}
                            <div class='projectsTitle'>
                            <p class='titleText'>Projects</p>
                            <!-- <img src='/projectsIcon.png' alt='projectsIcon' class='optionsIcon'> -->
                            </div>
                        {/if}
                        </button>
                    {/if}
                </div>

                <div class='rightOptionsDiv'>
                    {#if skills == true && skillsPage == false}
                        <button bind:this="{skillsTrans}" on:click = {() => buttonPressed('skills')} class='skillsDiv' style='background-image: url("/skillsBackground.png");' transition:fly={{ x: 100, y: -100, duration: 1000 }}>
                            {#if projects == true}
                            <div class='skillsTitle'>
                                <p class='titleText'>Skills</p>
                                <!-- <img src='/skillsIcon.png' alt='skillsIcon' class='optionsIcon'> -->
                            </div>
                            {/if}
                        </button>
                    {/if}
                    {#if skillsPage == true}
                    <div transition:fade class='skillsPageContainer'>
                        <div class= 'skillsTitleDiv'>
                            <p class='skillsTitleText'>Skills</p>
                        </div>
                        <div class='langDiv'>
                            <div class='frontEndDiv'>
                                <div class='frontEndTitle'>
                                    <p>Front End</p>
                                </div>
                                <div class = 'langContainer' transition:slide='{{axis: 'x', duration: 1000}}'>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>HTML / CSS</p>
                                    </div>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>JavaScript</p>
                                    </div>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>TypeScript</p>
                                    </div>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>Dart</p>
                                    </div>
                                </div>
                            </div>
                            <div class='toolsDiv'>
                                <div class='toolsTitle'>
                                    <p>Tools</p>
                                </div>
                                <div class='toolsLogoContainer'>
                                    <div class='toolsRow'>
                                        <img src='aws.png' alt='aws' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('aws')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                        <img src='colab.png' alt='colab' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('colab')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur> 
                                        <img src='figma.png' alt='figma' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('figma')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                        <img src='git.png' alt='git' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('git')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    </div>
                                    <div class= 'toolsRow'>
                                        <p class= 'hoverTitle' bind:this="{hoverTitle}">{toolsHover}</p>
                                    </div>
                                    <div class='toolsRow'>
                                        <img src='flutter.png' alt='flutter' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('flutter')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                        <img src='react.png' alt='react' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('react')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                        <img src='svelte.png' alt='svelte' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('svelte')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                        <img src='tensorflow.png' alt='awtensorflows' class='toolsLogoImg' on:mouseover = {() => mouseOverLogo('tensorflow')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    </div>
                                </div>
                            </div>
                            <div class='backEndDiv'>
                                <div class='backEndTitle'>
                                    <p>Back End</p>
                                </div>
                                <div class = 'langContainer' transition:slide='{{axis: 'x', duration: 1000}}' >
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>Python</p>
                                    </div>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>Java</p>
                                    </div>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>C / C++</p>
                                    </div>
                                    <div class= 'langBoxes'>
                                        <p class= 'langText'>Node.js</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class = 'infoDiv'>
                            <div class='daysProgDiv'>
                                <div class='infoNum'>
                                    <p style='margin: 0; top: 0;'>{daysProgStart}</p>
                                </div>
                                <div>
                                    <div class=infoTitle>
                                        <p class= infoText>Days Programming <br> Started March 26th 2022</p>
                                    </div>
                                </div>
                            </div>
                            <div class='gradYearDiv'>
                                <div class='infoNum'>
                                    <p style='margin: 0; top: 0;'>{gradYear}</p>
                                </div>
                                <div>
                                    <div class=infoTitle>
                                        <p class= infoText>Graduation Year <br> B.S. Computer Science</p>
                                    </div>
                                </div>
                            </div>
                            <div class='reposDiv'>
                                <div class='infoNum'>
                                    <p style='margin: 0; top: 0;'>{numRepos}</p>
                                </div>
                                <div>
                                    <div class=infoTitle>
                                        <p class= infoText>GitHub Repos <br> Note: Not all hosted are on GitHub</p>
                                    </div>
                                </div>
                            </div>
                            <div class='gpaDiv'>
                                <div class='infoNum'>
                                    <p style='margin: 0; top: 0;'>{gpa.toFixed(1)}</p>
                                </div>
                                <div>
                                    <div class=infoTitle>
                                        <p class= infoText>G.P.A. <br> 41 credits</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    {/if}
                    {#if contact == true && contactPage == false}
                        <button bind:this="{contactTrans}" on:click = {() => buttonPressed('contact')} class='contactDiv' style='background-image: url("/contactBackground.png"); background-position: center;' transition:fly={{ x: 100, y: 100, duration: 1000 }}>
                        {#if projects == true}
                        <div class='contactTitle'>
                            <p class='titleText'>Contact</p>
                        </div>
                        {/if}
                        </button>
                    {/if}
                    {#if contactPage == true}
                        <div class='contactPageContainer'>
                            <div class='contactBox'>
                                <div class= 'contactRow' style='order: 2;'>
                                    <a class='contactButton' href="https://github.com/ramankc6" target="_blank">
                                        <img src='github.png' alt='github' class='contactLogoImg'>
                                    </a>
                                    <a class='contactButton' href="https://www.linkedin.com/in/raman-khatri/" target="_blank">
                                        <img src='linkedin.png' alt='linkedin' class='contactLogoImg'>
                                    </a>
                                </div>
                                <div class= 'contactRow' style='order: 1; margin-right:2%;'>
                                    <a class='contactButton' href="mailto: ramankc24@gmail.com" target="_blank">
                                        <img src='email.png' alt='email' class='contactLogoImg'>
                                    </a>
                                </div>
                                <div class= 'contactPageTitle' style='order: -1;'>
                                    <div class = 'contactTitle' style='font-size:70px'>
                                        <p>Get in touch!</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    {/if}
                </div>
            </div>
        </div>
    {/if}
</body>

<svelte:window bind:scrollY={y} bind:innerWidth={userWidth} />