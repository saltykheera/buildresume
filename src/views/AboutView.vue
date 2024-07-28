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
import pdfMake from "pdfmake/build/pdfmake";
import { vfs as pdfFonts } from "pdfmake/build/vfs_fonts";
import { useCounterStore } from "../stores/counter";

pdfMake.vfs = pdfFonts;

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
  const docDefinition = {
    content: [
      { text: jsonData.value.userdetails.name, style: "header" },
      {
        text: "Job Profile: " + jsonData.value.userdetails.jobProfile,
        style: "subheader",
      },

      { text: "Contact Information", style: "subheader" },
      { text: "Email: " + jsonData.value.userContact.email },
      { text: "Phone: " + jsonData.value.userContact.phone },
      { text: "Location: " + jsonData.value.userContact.location },
      { text: "Twitter: " + jsonData.value.userContact.twitter },
      { text: "LinkedIn: " + jsonData.value.userContact.linkedin },

      { text: "Skills", style: "subheader" },
      { ul: jsonData.value.skills },

      { text: "Education", style: "subheader" },
      ...jsonData.value.Education.map((edu) => ({
        stack: [
          { text: edu.degree, style: "eduHeader" },
          { text: edu.institution },
          { text: `${edu.startDate} - ${edu.endDate}` },
          { text: edu.description },
        ],
      })),

      { text: "Achievements", style: "subheader" },
      ...jsonData.value.achievements.map((achievement) => ({
        stack: [
          { text: achievement.title, style: "achHeader" },
          { text: achievement.description },
        ],
      })),

      { text: "Work Experiences", style: "subheader" },
      ...jsonData.value.workExperiences.map((exp) => ({
        stack: [
          { text: exp.position, style: "expHeader" },
          { text: exp.company },
          { text: `${exp.startDate} - ${exp.endDate}` },
          { text: exp.description },
        ],
      })),

      { text: "Projects", style: "subheader" },
      ...jsonData.value.Projects.map((project) => ({
        stack: [
          { text: project.title, style: "projHeader" },
          { text: project.description },
          { text: `Link: ${project.link}`, link: project.link },
        ],
      })),
    ],
    styles: {
      header: {
        fontSize: 24,
        bold: true,
        marginBottom: 10,
      },
      subheader: {
        fontSize: 18,
        bold: true,
        marginTop: 10,
        marginBottom: 5,
      },
      eduHeader: {
        fontSize: 16,
        bold: true,
        marginTop: 5,
      },
      achHeader: {
        fontSize: 16,
        bold: true,
        marginTop: 5,
      },
      expHeader: {
        fontSize: 16,
        bold: true,
        marginTop: 5,
      },
      projHeader: {
        fontSize: 16,
        bold: true,
        marginTop: 5,
      },
    },
  };

  pdfMake.createPdf(docDefinition).download("resume.pdf");
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
