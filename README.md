# CV-site
Personal CV Website – My professional résumé and portfolio in HTML/CSS. Malik Irtaza CV – Online curriculum vitae built with HTML, CSS, and JavaScript.  Professional Portfolio – A single-page site to showcase my experience and skills.  Interactive Resume – Editable online CV for job applications.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Advanced Professional CV Builder</title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto&display=swap">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
  <style>
    body {
      font-family: 'Roboto', sans-serif;
      background: #f4f4f4;
      margin: 0;
      padding: 0;
    }
    .container {
      max-width: 1200px;
      margin: 20px auto;
      display: flex;
      gap: 20px;
    }
    .form-section, .cv-section {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      flex: 1;
    }
    .form-section input, .form-section textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 16px;
    }
    .form-section button {
      padding: 10px 15px;
      font-size: 16px;
      margin-top: 10px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
    }
    .cv-section {
      padding: 40px;
      background: white;
      color: #333;
      line-height: 1.6;
    }
    .cv-header {
      text-align: center;
      border-bottom: 2px solid #333;
      margin-bottom: 20px;
    }
    .cv-header h1 {
      margin: 0;
      font-size: 32px;
    }
    .cv-header p {
      margin: 5px 0;
    }
    .cv-section h2 {
      margin-top: 20px;
      font-size: 20px;
      border-bottom: 1px solid #ccc;
    }
    .cv-section ul {
      padding-left: 20px;
    }
    .cv-section li {
      margin-bottom: 8px;
    }
    #cv-photo {
      width: 120px;
      height: 150px;
      object-fit: cover;
      border-radius: 10px;
      margin: 10px auto;
      display: block;
    }
    #signature {
      width: 180px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="form-section">
      <h2>Fill Your CV Details</h2>
      <input type="file" id="photoInput" accept="image/*">
      <input type="text" id="name" placeholder="Full Name" />
      <input type="text" id="email" placeholder="Email" />
      <input type="text" id="phone" placeholder="Phone" />
      <input type="text" id="address" placeholder="Address" />
      <textarea id="summary" placeholder="Professional Summary"></textarea>
      <textarea id="education" placeholder="Education (use newline for multiple)"></textarea>
      <textarea id="experience" placeholder="Experience (use newline for multiple)"></textarea>
      <textarea id="skills" placeholder="Skills (comma separated)"></textarea>
      <textarea id="languages" placeholder="Languages Known (comma separated)"></textarea>
      <input type="file" id="signatureInput" accept="image/*">
      <button onclick="updateCV()">Preview CV</button>
      <button onclick="downloadCV()">Download PDF</button>
    </div>
    <div class="cv-section" id="cv">
      <div class="cv-header">
        <img id="cv-photo" src="" alt="Your Photo" style="display:none;"/>
        <h1 id="cv-name">Your Name</h1>
        <p id="cv-email">your.email@example.com</p>
        <p id="cv-phone">+123456789</p>
        <p id="cv-address">Your Address</p>
      </div>
      <h2>Professional Summary</h2>
      <p id="cv-summary">A brief summary about your professional experience and goals.</p>
      <h2>Education</h2>
      <ul id="cv-education"></ul>
      <h2>Experience</h2>
      <ul id="cv-experience"></ul>
      <h2>Skills</h2>
      <ul id="cv-skills"></ul>
      <h2>Languages</h2>
      <ul id="cv-languages"></ul>
      <div style="text-align:right;">
        <img id="signature" src="" alt="Signature" style="display:none;" />
      </div>
    </div>
  </div>
  <script>
    function updateCV() {
      document.getElementById("cv-name").innerText = document.getElementById("name").value;
      document.getElementById("cv-email").innerText = document.getElementById("email").value;
      document.getElementById("cv-phone").innerText = document.getElementById("phone").value;
      document.getElementById("cv-address").innerText = document.getElementById("address").value;
      document.getElementById("cv-summary").innerText = document.getElementById("summary").value;

      const educationLines = document.getElementById("education").value.split("\n");
      const educationList = document.getElementById("cv-education");
      educationList.innerHTML = "";
      educationLines.forEach(line => {
        if (line.trim()) {
          const li = document.createElement("li");
          li.textContent = line;
          educationList.appendChild(li);
        }
      });

      const experienceLines = document.getElementById("experience").value.split("\n");
      const experienceList = document.getElementById("cv-experience");
      experienceList.innerHTML = "";
      experienceLines.forEach(line => {
        if (line.trim()) {
          const li = document.createElement("li");
          li.textContent = line;
          experienceList.appendChild(li);
        }
      });

      const skills = document.getElementById("skills").value.split(",");
      const skillList = document.getElementById("cv-skills");
      skillList.innerHTML = "";
      skills.forEach(skill => {
        if (skill.trim()) {
          const li = document.createElement("li");
          li.textContent = skill.trim();
          skillList.appendChild(li);
        }
      });

      const languages = document.getElementById("languages").value.split(",");
      const langList = document.getElementById("cv-languages");
      langList.innerHTML = "";
      languages.forEach(lang => {
        if (lang.trim()) {
          const li = document.createElement("li");
          li.textContent = lang.trim();
          langList.appendChild(li);
        }
      });

      const photoInput = document.getElementById("photoInput").files[0];
      const cvPhoto = document.getElementById("cv-photo");
      if (photoInput) {
        const reader = new FileReader();
        reader.onload = function (e) {
          cvPhoto.src = e.target.result;
          cvPhoto.style.display = "block";
        };
        reader.readAsDataURL(photoInput);
      }

      const signInput = document.getElementById("signatureInput").files[0];
      const signature = document.getElementById("signature");
      if (signInput) {
        const reader = new FileReader();
        reader.onload = function (e) {
          signature.src = e.target.result;
          signature.style.display = "inline-block";
        };
        reader.readAsDataURL(signInput);
      }
    }

    function downloadCV() {
      const element = document.getElementById("cv");
      html2pdf().from(element).save("Advanced_CV.pdf");
    }
  </script>
</body>
</html>
