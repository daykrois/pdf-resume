<script setup>
import * as htmlToImage from 'html-to-image';
import jsPDF from 'jspdf';

function resumeToPDF(){
    const resume = document.getElementById('resume');
    htmlToImage.toCanvas(resume).then(function (canvas) {
          // document.body.appendChild(canvas);
          var contentWidth = canvas.width;
          var contentHeight = canvas.height;

          //一页pdf显示html页面生成的canvas高度;
          var pageHeight = contentWidth / 592.28 * 841.89;
          //未生成pdf的html页面高度
          var leftHeight = contentHeight;
          //页面偏移
          var position = 0;
          //a4纸的尺寸[595.28,841.89]，html页面生成的canvas在pdf中图片的宽高
          var imgWidth = 595.28;
          var imgHeight = 592.28 / contentWidth * contentHeight;

          var pageData = canvas.toDataURL('image/jpeg', 1.0);

          var pdf = new jsPDF('', 'pt', 'a4');

          //有两个高度需要区分，一个是html页面的实际高度，和生成pdf的页面高度(841.89)
          //当内容未超过pdf一页显示的范围，无需分页
          if (leftHeight < pageHeight) {
            console.log(imgWidth, imgHeight, 'imgWidth, imgHeight')
            pdf.addImage(pageData, 'JPEG', 0, 0, imgWidth, imgHeight);
          } else {
            while (leftHeight > 0) {
              pdf.addImage(pageData, 'JPEG', 0, position, imgWidth, imgHeight)
              leftHeight -= pageHeight;
              position -= 841.89;
              //避免添加空白页
              if (leftHeight > 0) {
                pdf.addPage();
              }
            }
          }
          pdf.save(`resume.pdf`);
        }).catch((err) => {
          console.log(err)
        //   message.warning("导出PDF失败")
        });
}
</script>

<template>
    <div id="resume">
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

    <button @click="resumeToPDF()">下载pdf</button>

</template>

<style>
#pdf {
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