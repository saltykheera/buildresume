<template>
  <div id="app">
    <h1>{{ jsonData.userdetails.name }}</h1>
    <div class="section">
      <h2>Job Profile: {{ jsonData.userdetails.jobProfile }}</h2>
    </div>

    <div class="section">
      <h2>Contact Information</h2>
      <p>Email: {{ jsonData.userContact.email }}</p>
      <p>Phone: {{ jsonData.userContact.phone }}</p>
      <p>Location: {{ jsonData.userContact.location }}</p>
      <p>Twitter: {{ jsonData.userContact.twitter }}</p>
      <p>LinkedIn: {{ jsonData.userContact.linkedin }}</p>
    </div>

    <div class="section">
      <h2>Skills</h2>
      <ul>
        <li v-for="skill in jsonData.skills" :key="skill">{{ skill }}</li>
      </ul>
    </div>

    <div class="section">
      <h2>Education</h2>
      <div v-for="(edu, index) in jsonData.Education" :key="index">
        <h3>{{ edu.degree }}</h3>
        <p>{{ edu.institution }}</p>
        <p>{{ edu.startDate }} - {{ edu.endDate }}</p>
        <p>{{ edu.description }}</p>
      </div>
    </div>

    <div class="section">
      <h2>Achievements</h2>
      <div v-for="(achievement, index) in jsonData.achievements" :key="index">
        <h3>{{ achievement.title }}</h3>
        <p>{{ achievement.description }}</p>
      </div>
    </div>

    <div class="section">
      <h2>Work Experiences</h2>
      <div v-for="(exp, index) in jsonData.workExperiences" :key="index">
        <h3>{{ exp.position }}</h3>
        <p>{{ exp.company }}</p>
        <p>{{ exp.startDate }} - {{ exp.endDate }}</p>
        <p>{{ exp.description }}</p>
      </div>
    </div>

    <div class="section">
      <h2>Projects</h2>
      <div v-for="(project, index) in jsonData.Projects" :key="index">
        <h3>{{ project.title }}</h3>
        <p>{{ project.description }}</p>
        <p>
          Link: <a :href="project.link">{{ project.link }}</a>
        </p>
      </div>
    </div>

    <!-- Button to generate PDF -->
    <button @click="generatePDF">Generate PDF</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
import jsPDF from "jspdf";
import html2canvas from "html2canvas";
import { useCounterStore } from "../stores/counter";

const store = useCounterStore();

// Extract resume data from the store
const jsonData = ref({
  userdetails:
    store.ResumeData.find((item) => "userdetails" in item)?.userdetails || {},
  userContact:
    store.ResumeData.find((item) => "userContact" in item)?.userContact || {},
  skills: store.ResumeData.find((item) => "skills" in item)?.skills || [],
  Education:
    store.ResumeData.find((item) => "Education" in item)?.Education || [],
  achievements:
    store.ResumeData.find((item) => "achievements" in item)?.achievements || [],
  workExperiences:
    store.ResumeData.find((item) => "workExperiences" in item)
      ?.workExperiences || [],
  Projects: store.ResumeData.find((item) => "Projects" in item)?.Projects || [],
});

const generatePDF = () => {
  const element = document.getElementById("app");

  const options = {
    scale: 4,
    windowWidth: element.scrollWidth,
    windowHeight: element.scrollHeight,
    logging: true,
  };

  html2canvas(element, options).then((canvas) => {
    const imgData = canvas.toDataURL("image/jpeg", 1.0);
    const pdf = new jsPDF("p", "mm", "a4");
    const width = pdf.internal.pageSize.getWidth();
    const height = pdf.internal.pageSize.getHeight();

    pdf.addImage(imgData, "JPEG", 0, 0, width, height, "", "FAST");
    pdf.save("document.pdf");
  });
};
</script>

<style scoped>
#app {
  font-family: Arial, sans-serif;
  padding: 20px;
  width: 100%;
}

.section {
  margin-bottom: 20px;
}

h1,
h2,
h3 {
  color: #333;
}

p {
  color: #555;
  margin: 5px 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
