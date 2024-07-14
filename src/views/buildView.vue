<template>
  <div class="main d-flex" style="gap: 20px">
    <h1>this is the build page</h1>
    <v-card>
      <v-card-title> User Detail </v-card-title>
      <v-card-text>
        <v-text-field label="Name" variant="outlined"></v-text-field>
        <v-text-field label="Job Profile" variant="outlined"></v-text-field>
      </v-card-text>
    </v-card>
    <v-card>
      <v-card-title> User Contact </v-card-title>
      <v-card-text>
        <v-text-field label="Email" variant="outlined"></v-text-field>
        <v-text-field label="Phone" variant="outlined"></v-text-field>
        <v-text-field label="Location" variant="outlined"></v-text-field>
        <v-text-field label="Twitter" variant="outlined"></v-text-field>
        <v-text-field label="LinkedIn" variant="outlined"></v-text-field>
      </v-card-text>
    </v-card>
    <v-card>
      <v-card-title>Work Experience</v-card-title>
      <v-card-text>
        <v-text-field label="Company" variant="outlined"></v-text-field>
        <v-text-field label="Position" variant="outlined"></v-text-field>
        <v-text-field label="Start Date" variant="outlined"></v-text-field>
        <v-text-field label="End Date" variant="outlined"></v-text-field>
        <v-textarea
          label="Description"
          rows="4"
          variant="outlined"
        ></v-textarea>
      </v-card-text>
      <v-card-action>
        <v-btn color="primary" @click="addWorkExperience"
          >Add Work Experience</v-btn
        >
      </v-card-action>
    </v-card>
    <v-card>
      <v-card-title>Skills</v-card-title>
      <v-card-text>
        <v-text-field
          label="Skill"
          variant="outlined"
          v-for="(skill, index) in skills"
          :key="index"
          :placeholder="index === 0 ? 'Enter skill' : ''"
        />
        <v-btn color="primary" @click="addSkill">Add Skill</v-btn>
      </v-card-text>
    </v-card>
    <v-card>
      <v-card-title> Education </v-card-title>
      <v-card-text>
        <v-text-field label="Degree" variant="outlined"></v-text-field>
        <v-text-field label="Institution" variant="outlined"></v-text-field>
        <v-text-field label="Start Date" variant="outlined"></v-text-field>
        <v-text-field label="End Date" variant="outlined"></v-text-field>
        <v-textarea
          label="Description"
          rows="4"
          variant="outlined"
        ></v-textarea>
      </v-card-text>
      <v-card-action>
        <v-btn color="primary" @click="addEducation">Add Education</v-btn>
      </v-card-action>
    </v-card>
    <v-card>
      <v-card-title> Achivements </v-card-title>
      <v-card-text>
        <v-select
          label="Select"
          :items="['1', '2', '3', '4', '5', '6']"
          variant="outlined"
        ></v-select>
        <v-text-field
          label="Achievement Title"
          variant="outlined"
        ></v-text-field>
        <v-textarea
          label="Achievement Description"
          rows="4"
          variant="outlined"
        ></v-textarea>
        <v-btn color="success">SAVE</v-btn>
      </v-card-text>
    </v-card>
    <v-card>
      <v-card-title> Projects </v-card-title>
      <v-card-text>
        <v-select
          label="Number of Achievements"
          :items="['1', '2', '3', '4', '5', '6']"
          variant="outlined"
        ></v-select>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {};
</script>

<style></style>
