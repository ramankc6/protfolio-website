
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
let selectedProject = 'none';

//Const Text Declaration
const fullText = ["Hey Everyone!", "My name is Raman Khatri Chhetri"];
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
let projectsPage = false
//-------Start onMount-------//

//When the user loads the website it calls cusor Annimation which starts the typing annimation
onMount(async () => {
    // alert('This website is still under construction, please excuse the mess')
    cursorAnnimation();
    imageResizer();
    updateOptionsDiv();
    // drake();
    y = 0;
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
            showScroller = true;
        }
    }
}

// function mouseAnnimation() {
//     if (mouseAnnimationIndex % 2 == 0) {
//         showScroller = false
//         mouseAnnimationIndex++
//         setTimeout(mouseAnnimation, 600)
//     } else{
//         showScroller = true
//         mouseAnnimationIndex++
//         setTimeout(mouseAnnimation, 1000)
//     }
// }

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
    if (y > 900 && y < 1700) {
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
        projectsPage = true;
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
        projectsPage = false;

    }
    setTimeout(updateOptionsDiv, 0)
}

function backButton(pressedButton) {
    if (pressedButton == 'back') {
        y = 1700;
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
        projectsPage = false;
    }
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

function mouseOverProjects(project) {
    if (project == 'none'){
        selectedProject = 'none'
    } else if (project == 'portfolio') {
        selectedProject = 'portfolio'
    } else if (project == 'phitNest') {
        selectedProject = 'phitNest'
    } else if (project == 'wordle') {
        selectedProject = 'wordle'
    } else if (project == 'co2') {
        selectedProject = 'co2'
    } else if (project == 'noFearSpeak') {
        selectedProject = 'noFearSpeak'
    }
}  
</script>



<style>

@import url('https://fonts.cdnfonts.com/css/cascadia-code');
@import url('https://fonts.googleapis.com/css2?family=Palanquin+Dark&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro&display=swap');

body{
    background-color: #1e1e1e;
    min-height: 3500px;
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
    border-radius: 10%;
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
    aspect-ratio: 307.38/520.33;
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
    animation: jump 0.7s infinite alternate;
    margin-top: 2%;
}
@keyframes jump {
0% {
  transform: translateY(0);
}
100% {
  transform: translateY(-15px);
}
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
    aspect-ratio: 1/1;
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
    background-image: url('/contactBackground.png');
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
    aspect-ratio: 1/1;
}
.contactButton {
    background: none;
    border: none;
    height:10%;
    margin-top: 60%;
    aspect-ratio: 1/1;
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
.contactDiv {
    background-image: url("/contactBackground.png");
    background-position: center;
}

.skillsDiv {
    background-image: url("/skillsBackground.png");
}

.resumeDiv {
    background-image: url("/resumeBackground.png");
}

#githubLogo {
    aspect-ratio: 4/3;
}
.contactTitleDiv {
    color: black;
    width: 100%;
    text-align: center;
    font-size: 70px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    margin-top: 0%;
}

.projectsPageContainer {
    z-index: 9;
    display: flex;
    position: fixed;
    width: 100%;
    height: 100%;
    /* right: 5.1%; */
    /* bottom: 5vh;
    top: 0.5vh; */
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    left:0;
    top:0;
    right:0;
    bottom:0;
    
}

.projectsTitleDiv {
    color: white;
    width: 100%;
    text-align: center;
    font-size: 70px;
    margin: 0%;
    font-family: 'Palanquin Dark', sans-serif;
    margin-top: 0%;
}

.projectsLogosContainer {
    display: flex;
    flex-direction: row;
    width: 100vw;
    height: 40%;
    justify-content: space-evenly;
}

.portfolioDiv,
.phitNestDiv,
.wordleDiv,
.co2Div,
.noFearSpeakDiv {
    width: 10%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    transition: 0.5s;
}

.projectLogo {
    width: 100%;
    height: 100%;
    aspect-ratio: 1/1;
}

.discription {
    width: 95%;
    height: 100%;
    transition: 0.5s;
    margin-bottom: 3%;
    margin-top:3%;
    border-radius: 10px;
    border: 3px solid white;
    color: white;
}

.linkImg {
    width: 4%;
    height: 4%;
    aspect-ratio: 1/1;

}
.discriptionText {
    font-size: 15px;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    text-align: left;
    margin-left: 2%;
    margin-right: 2%;
}
.discriptionTitle {
    font-size: 20px;
    font-family: 'Palanquin Dark', sans-serif;
    text-align: left;
    margin-left: 2%;
    margin-right: 2%;
}

.techStack {
    margin-left: 2%;
    margin-right: 2%;
}
.discription_Links{
    margin-left: 2%;
    margin-right: 2%;
}

.projectTitle {
    font-size: 20px;
    font-family: 'Palanquin Dark', sans-serif;
    color: white;
    text-align: center;
}
.linkImg:hover {
    transform: scale(0.9);
    transition: 0.5s;
}

.back {
    height: 5%;
    margin-top: 5%;
    transition: 0.5s;
    z-index: 100;
    position: fixed;
    outline: none;
    border: 2px solid white;
    background: none;
    color: black;
    margin-left: 5%;
    background-color: lightgoldenrodyellow;
    font: 20px 'Palanquin Dark', sans-serif;
    border-radius: 50px;
}
.backText {
    padding: 0px;
    margin: 0px;
}

.back:hover {
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
    .contactDiv {
        background-image: url('/mobileContact.png');
        background-position: top;
    }
    .skillsDiv {
    background-image: url("/mobileSkills.png");
    }
    .resumeDiv {
        background-image: url("/mobileResume.png");
    }
    .contactBox {
        background-image: url('/mobileContact.png');
        background-size: 100%;
        background-position: 4% 4%;
        background-repeat: no-repeat;
        width: 85%;
        height: 95%;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        border-radius:60px/5%;
    }
    .contactLogoImg {
        background:none;
        width: 100%;
        height: 100%;
        aspect-ratio: 1/1;
    }
    .contactButton {
        background: none;
        border: none;
        height:100%;
        margin-top: 14%;
        margin-left: 3%;
        /* background-color: white; */
        border-radius: 10%;

    }
    .contactRow {
        display: flex;
        flex-direction: column;
        width: 100%;
        height: 10%;
        align-items: center;
        margin-top: 14%;
        /* align-items: flex-start;
        justify-content: flex-start; */
    }
    .contactTitleDiv {
        color: black;
        width: 100%;
        text-align: center;
        font-size: 40px;
        margin: 0%;
        font-family: 'Palanquin Dark', sans-serif;
        margin-top: 0%;
    }
    .contactPageTitle {
    padding-right: 0%;
    width:100%;
    }
    .contactTitleText {
        margin: 0%;
        padding-bottom: 40%;
    }
    .projectTitle {
        font-size: 10px;
    }
    .hoverTitle {
        font-size: 20px;
    }
    .introText {
        font-size: 4vw;
    }
    .scrollerContainer {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
        margin-left: 0%;
    }
    .headshotImg {
        min-height: 40vh;
        min-width: 31.25vw;
    }
}   


</style>

<body>
    {#if projectsPage || contactPage || skillsPage || resumePage}
    <button class = 'back' on:click = {() => backButton('back')}>
        <p class = 'backText'>Back</p>
    </button>
    {/if}
    <!-- <audio controls autoplay bind:this={audio}>
        <source src='/music.mp3' type='audio/mp3'>
    </audio> -->
    {#if y > 50 && y < 1700}
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
                        <div class='scrollerContainer'>
                            <img src= {scrollImg} alt='mouseScroll' class = 'mouseImg'>
                        </div>
                    {/if}
                </div>
            </div>
        </div>
    {/if}
    {#if y > 50 && y < 1200}
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
                    <p>I am a full-stack Software Engineer with experince in web development, mobile development, data science and ML. I am always looking for new oppurtunies to improve my skills through projects and internships. You can navigate my portfolio by scrolling up and down!</p>
                </div>
            </div>
        </div>
    {/if}
    {#if y > 1600}
        <div class ='optionsPage'>
            <div class='optionsDiv'>
                <div class='leftOptionsDiv'>
                    {#if resume == true && resumePage == false}
                        <button bind:this="{resumeTrans}" on:click = {() => buttonPressed('resume')} class='resumeDiv' in:fly={{ x: -100, y: -100, duration: 1000 }} out:fade>
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
                    {#if projects == true && projectsPage == false}
                        <button bind:this="{projectsTrans}" on:click = {() => buttonPressed('projects')} class='projectsDiv' style='background-image: url("/projectBackground.png");' transition:fly={{ x: -100, y: 100, duration: 1000 }}>
                        {#if resume == true}
                            <div class='projectsTitle'>
                            <p class='titleText'>Projects</p>
                            <!-- <img src='/projectsIcon.png' alt='projectsIcon' class='optionsIcon'> -->
                            </div>
                        {/if}
                        </button>
                    {/if}
                    {#if projectsPage == true}
                    <div transition:fade class='projectsPageContainer'>
                            <div class='projectsTitleDiv'>
                                <p class='projectsTitleText'>Projects</p>
                            </div>
                            <div class='projectsLogosContainer'>
                                <div class='portfolioDiv' on:mouseover = {() => mouseOverProjects('portfolio')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    <img src='/headshot.png' alt='headshot' class='projectLogo'>
                                    <p class='projectTitle'>Portfolio</p>
                                </div>
                                <div class='phitNestDiv' on:mouseover = {() => mouseOverProjects('phitNest')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    <img src='/phitnest.png' alt='headshot' class='projectLogo'>
                                    <p class='projectTitle'>PhitNest</p>
                                </div>
                                <div class='wordleDiv' on:mouseover = {() => mouseOverProjects('wordle')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    <img src='/wordle.png' alt='headshot' class='projectLogo'>
                                    <p class='projectTitle'>Wordle Solver</p>
                                </div>
                                <div class='co2Div' on:mouseover = {() => mouseOverProjects('co2')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    <img src='/co2.png' alt='headshot' class='projectLogo'>
                                    <p class='projectTitle'>CO2 Calculator</p>
                                </div>
                                <div class='noFearSpeakDiv' on:mouseover = {() => mouseOverProjects('noFearSpeak')} on:mouseout = {() => mouseOverLogo('none')} on:focus on:blur>
                                    <img src='/nofearspeak.png' alt='headshot' class='projectLogo'>
                                    <p class='projectTitle'>NoFearSpeak</p>
                                </div>
                            </div>
                            {#if selectedProject == 'none'}
                            <div class = 'discription'>
                                <h2 class='discriptionTitle'> Hover Over An Image</h2>
                                <p class='discriptionText'></p>
                                <h3><b></b></h3>
                                <div class= 'discription_Links'>
                                </div>
                            </div>
                            {/if}
                            {#if selectedProject == 'portfolio'}
                            <div class = 'discription'>
                                <h2 class='discriptionTitle'>Portfolio</h2>
                                <p class='discriptionText'>This is my first personal web development project. My intention was to create a page where I can showcase all the new 
                                    projects I am working on and to also have a place where I can share my resume and contact information. I used Svelte to create this page and
                                    I am very happy with the results. I am looking forward to adding more projects to this page and to continue to improve the design and functionality.
                                </p>
                                <p class= 'techStack'><b>Tech Stack: </b>HTML, CSS, JavaScript, Svelte, Netlify</p>
                                <div class= 'discription_Links'>
                                    <a href='https://github.com/ramankc6/protfolio-website' target='_blank' class='discriptionLink'><img src='/github.png' alt='github' class = 'linkImg'></a>
                                    <a href='https://ramankhatri.com/' target='_blank' class='discriptionLink'><img src='/link.png' alt='github'class = 'linkImg'></a>
                                </div>
                            </div>
                            {/if}
                            {#if selectedProject == 'phitNest'}
                            <div class = 'discription'>
                                <h2 class='discriptionTitle'>PhitNest</h2>
                                <p class='discriptionText'>PhitNest is a mobile app start-up that I am interning for. I initially worked most only on their mobile development team but shifted to Web Dev.
                                    As a Web Development Intern, I am indepently creating and maintaining the company's website. Though the design is created by the marketing team, most if not all the development is done by me.
                                    I am very excited to be working for PhitNest and I am looking forward to seeing 
                                    what the future holds for the company.
                                </p>
                                <p class= 'techStack'><b>Tech Stack: </b>HTML, CSS, TypeScript, React, Svelte, AWS, Git</p>
                                <div class= 'discription_Links'>
                                    <a href='https://phitnest.com' target='_blank' class='discriptionLink'><img src='/link.png' alt='github' class = 'linkImg'></a>
                                </div>
                            </div>
                            {/if}
                            {#if selectedProject == 'wordle'}
                            <div class = 'discription'>
                                <h2 class='discriptionTitle'>Wordle Solver</h2>
                                <p class='discriptionText'>This is a algorytm that uses entropy and other sorting techniques to find answers to wordle. 
                                    I used techniques like cashe, parallelization and heuristics to make this program as fast as possible without sacrificing accuracy.
                                    I learned alot about data structures and alorythms while working on this project. I was able to achive a 95% accuracy rate after running 2000 tests in 20 seconds.
                                    I am very proud of this project and I am looking forward to taking on more projects like this in the future since it really helped peak my interest in data structures and algorithms.
                                </p>
                                <p class= 'techStack'><b>Tech Stack: </b>Python, Google Colab, Git</p>
                                <div class= 'discription_Links'>
                                    <a href='https://github.com/ramankc6/wordle-solver' target='_blank' class='discriptionLink'><img src='/github.png' alt='github' class = 'linkImg'></a>
                                </div>
                            </div>
                            {/if}
                            {#if selectedProject == 'co2'}
                            <div class = 'discription'>
                                <h2 class='discriptionTitle'>Co2 Emissions Algorytm</h2>
                                <p class='discriptionText'>This project was my introduction to machine learning and it was love at first pipeline. I made this during
                                    VTHacks22, where it garnered the attention of the Hackathon's main sponsor, Capgemini. Though I was on a team for this Hackathon, all work done for this algorythm was independently done by me.
                                    I was able to get a 88% accuracy rate. I used a linear regression model to predict the amount of co2 emissions
                                    a car would produce based on the cars make, model, year, and fuel type. This project inspired me to continue to learn more about machine learning and have been working on a few other related projects since.
                                </p>
                                <p class= 'techStack'><b>Tech Stack: </b>Python, Tensorflow, Google Colab</p>
                                <div class= 'discription_Links'>
                                    <a href='https://github.com/ramankc6/CO2-Prediction-Algorithm' target='_blank' class='discriptionLink'><img src='/github.png' alt='github' class = 'linkImg'></a>
                                </div>
                            </div>
                            {/if}
                            {#if selectedProject == 'noFearSpeak'}
                            <div class = 'discription'>
                                <h2 class='discriptionTitle'>NoFearSpeak</h2>
                                <p class='discriptionText'>NoFearSpeak was a group project for a Hackathon called HackViolet. It is a cross platform app that allows
                                    users to anonymously report harassment in the work place. I played a product manager role during this project. I helped my teammate with 
                                    the design while also working on developing the front end using Flutter. I also created the back-end which allowed the app to 
                                    communicate with the database and allowed user to dynamically search though the companies and the people.
                                </p>
                                <p class= 'techStack'><b>Tech Stack: </b>Dart, Flutter, Firebase, Xcode, Google Cloud, Git</p>
                                <div class= 'discription_Links'>
                                    <a href='https://github.com/ramankc6/NoFearSpeak' target='_blank' class='discriptionLink'><img src='/github.png' alt='github' class = 'linkImg'></a>
                                    <a href='https://devpost.com/software/safenest-j0x5bi' target='_blank' class='discriptionLink'><img src='/devpost.png' alt='github'class = 'linkImg'></a>
                                </div>
                            </div>
                            {/if}
                    </div>
                    {/if}
                </div>
                <div class='rightOptionsDiv'>
                    {#if skills == true && skillsPage == false}
                        <button bind:this="{skillsTrans}" on:click = {() => buttonPressed('skills')} class='skillsDiv' transition:fly={{ x: 100, y: -100, duration: 1000 }}>
                            {#if projects == true}
                            <div class='skillsTitle'>
                                <p class='titleText'>Skills</p>
                                <!-- <img src='/skillsIcon.png' alt='skillsIcon' class='optionsIcon'> -->
                            </div>
                            {/if}
                        </button>
                    {/if}
                    {#if skillsPage == true }
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
                        <button bind:this="{contactTrans}" on:click = {() => buttonPressed('contact')} class='contactDiv' transition:fly={{ x: 100, y: 100, duration: 1000 }}>
                        {#if projects == true}
                        <div class='contactTitle'>
                            <p class='titleText'>Contact</p>
                        </div>
                        {/if}
                        </button>
                    {/if}
                    {#if contactPage == true}
                        <div class='contactPageContainer' transition:fade>
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
                                    <a class='contactButton' id='githubLogo' href="mailto: ramankc24@gmail.com" target="_blank">
                                        <img src='email.png' alt='email' class='contactLogoImg'>
                                    </a>
                                </div>
                                <div class= 'contactPageTitle' style='order: -1;'>
                                    <div class = 'contactTitleDiv'>
                                        <p class='contactTitleText'>Get In Touch!</p>
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