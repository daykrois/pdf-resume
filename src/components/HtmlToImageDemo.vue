<script setup>
import * as htmlToImage from 'html-to-image';

const divList = [];

function resumeToCanvas(divList,filename) {
    const resume1 = document.getElementById('resume1');
    const resume2 = document.getElementById('resume2');
    htmlToImage.toCanvas(resume1).then(function (canvas) {
        var dataURL = canvas.toDataURL('image/png'); 
        var img = new Image();
        img.src = dataURL;
        var link = document.createElement('a');
        link.href = dataURL;
        link.download = `${filename}.png`; 
        link.click(); 
        link.remove(); 
    });

    htmlToImage.toCanvas(resume2).then(function (canvas) {
        var dataURL = canvas.toDataURL('image/png'); 
        var img = new Image();
        img.src = dataURL;
        var link = document.createElement('a');
        link.href = dataURL;
        link.download = `${filename}.png`; 
        link.click(); 
        link.remove(); 
    });
}





</script>

<template>
    <div id="resume1">
        <div class="container">
            <h1>个人简历</h1>

            <div class="section">
                <h2>Contact Information</h2>
                <div class="info">
                    <label>Name:</label> John Doe
                </div>
                <div class="info">
                    <label>Email:</label> john.doe@example.com
                </div>
                <div class="info">
                    <label>Phone:</label> (123) 456-7890
                </div>
            </div>

            <div class="section">
                <h2>Work Experience</h2>
                <ul class="work-experience">
                    <li>
                        <h3>Software Engineer at XYZ Corp</h3>
                        <p>Jan 2020 - Present</p>
                        <p>Developed and maintained web applications using modern JavaScript frameworks.</p>
                    </li>
                    <li>
                        <h3>Intern at ABC Inc</h3>
                        <p>Jun 2019 - Aug 2019</p>
                        <p>Assisted in debugging and testing software applications.</p>
                    </li>
                </ul>
            </div>

            <div class="section">
                <h2>Education</h2>
                <ul class="education">
                    <li>
                        <h3>Bachelor of Science in Computer Science</h3>
                        <p>University of XYZ, 2019</p>
                    </li>
                </ul>
            </div>
        </div>
    </div>
    <div id="resume2">
        <div class="container">
            <h1>个人简历</h1>

            <div class="section">
                <h2>Contact Information</h2>
                <div class="info">
                    <label>Name:</label> John Doe
                </div>
                <div class="info">
                    <label>Email:</label> john.doe@example.com
                </div>
                <div class="info">
                    <label>Phone:</label> (123) 456-7890
                </div>
            </div>

            <div class="section">
                <h2>Work Experience</h2>
                <ul class="work-experience">
                    <li>
                        <h3>Software Engineer at XYZ Corp</h3>
                        <p>Jan 2020 - Present</p>
                        <p>Developed and maintained web applications using modern JavaScript frameworks.</p>
                    </li>
                    <li>
                        <h3>Intern at ABC Inc</h3>
                        <p>Jun 2019 - Aug 2019</p>
                        <p>Assisted in debugging and testing software applications.</p>
                    </li>
                </ul>
            </div>

            <div class="section">
                <h2>Education</h2>
                <ul class="education">
                    <li>
                        <h3>Bachelor of Science in Computer Science</h3>
                        <p>University of XYZ, 2019</p>
                    </li>
                </ul>
            </div>
        </div>
    </div>

    <button @click="resumeToCanvas()">下载截图</button>

</template>

<style>
#resume1 {
    width: 794px;
    height: 1123px;
    background-color: #fff;
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    margin: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
    text-rendering: geometricPrecision;
}

#resume2 {
    width: 794px;
    height: 1123px;
    background-color: #fff;
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    margin: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
    text-rendering: geometricPrecision;
}

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

.container {
    max-width: 800px;
    margin: auto;
    padding: 20px;
}

h1 {
    text-align: center;
}

.section {
    margin-bottom: 20px;
}

.section h2 {
    border-bottom: 1px solid #000;
    padding-bottom: 5px;
}

.info {
    margin-bottom: 10px;
}

.info label {
    font-weight: bold;
}

.work-experience,
.education {
    list-style-type: none;
    padding: 0;
}

.work-experience li,
.education li {
    margin-bottom: 10px;
}

.work-experience li p,
.education li p {
    margin: 5px 0;
}
</style>