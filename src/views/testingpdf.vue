<template>
  <div>
    <button @click="downloadPdf">Download PDF</button>
  </div>
</template>

<script>
import pdfMake from "pdfmake/build/pdfmake";
import pdfFonts from "pdfmake/build/vfs_fonts";

pdfMake.vfs = pdfFonts.pdfMake.vfs;

export default {
  name: "PdfDownload",
  methods: {
    downloadPdf() {
      const jsonData = {
        name: "John Doe",
        contact: {
          email: "john.doe@example.com",
          phone: "123-456-7890",
        },
        skills: ["JavaScript", "Vue.js", "Node.js"],
        education: [
          {
            degree: "B.Sc. Computer Science",
            institution: "University A",
            year: 2020,
          },
          {
            degree: "M.Sc. Computer Science",
            institution: "University B",
            year: 2023,
          },
        ],
      };

      const docDefinition = {
        content: [
          { text: "Name: " + jsonData.name, style: "header" },
          { text: "Contact Information", style: "subheader" },
          "Email: " + jsonData.contact.email,
          "Phone: " + jsonData.contact.phone,
          { text: "Skills", style: "subheader" },
          {
            ul: jsonData.skills.map((skill) => skill),
          },
          { text: "Education", style: "subheader" },
          {
            table: {
              headerRows: 1,
              widths: ["*", "*", "*"],
              body: [
                ["Degree", "Institution", "Year"],
                ...jsonData.education.map((edu) => [
                  edu.degree,
                  edu.institution,
                  edu.year,
                ]),
              ],
            },
          },
        ],
        styles: {
          header: {
            fontSize: 18,
            bold: true,
          },
          subheader: {
            fontSize: 14,
            bold: true,
          },
        },
      };

      pdfMake.createPdf(docDefinition).download("output.pdf");
    },
  },
};
</script>
