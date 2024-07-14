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

    <!-- Render other sections like Education, Achievements, Work Experiences, Projects -->

    <!-- Button to generate PDF -->
    <button @click="generatePDF">Generate PDF</button>
  </div>
</template>

<script>
import jsPDF from "jspdf";
import html2canvas from "html2canvas";

export default {
  name: "App",
  data() {
    return {
      jsonData: {
        userdetails: { name: "x", jobProfile: "x" },
        userContact: {
          email: "xx",
          phone: "xx",
          location: "xx",
          twitter: "xx",
          linkedin: "xx",
        },
        skills: ["x", "y"],
        Education: [
          {
            degree: "s",
            institution: "i",
            startDate: "s",
            endDate: "e",
            description: "d",
          },
        ],
        achievements: [{ title: "av", description: "ad" }],
        workExperiences: [
          {
            company: "cx",
            position: "p",
            startDate: "sd",
            endDate: "ed",
            description: "des",
          },
        ],
        Projects: [{ title: "s", link: "s", description: "des" }],
      },
    };
  },
  methods: {
    generatePDF() {
      const element = document.getElementById("app");

      html2canvas(element).then((canvas) => {
        const imgData = canvas.toDataURL("image/png");
        const pdf = new jsPDF("p", "mm", "a4");
        const width = pdf.internal.pageSize.getWidth();
        const height = pdf.internal.pageSize.getHeight();
        pdf.addImage(imgData, "JPEG", 0, 0, width, height);
        pdf.save("document.pdf");
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  padding: 20px;
}

.section {
  margin-bottom: 20px;
}

h1,
h2 {
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
