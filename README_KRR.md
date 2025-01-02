# Homework 1: Knowledge Representation and Reasoning (KR&R)

## Overview
This project focuses on using Description Logic (DL) to model real-world entities and their relationships, providing a formal way to represent medical environments including persons, doctors, patients, departments, and treatments.

---

## Section 1: Diagram
A diagram (not included in the text) likely visualizes the relationships and hierarchies described in subsequent sections. The diagram typically illustrates how entities like doctors, patients, departments, and treatments interact.

---

## Section 2: Description Logic

### Concepts (Classes)
These define the main entities within the system:
- **Person**: Every entity classified as a person.  
  `Person ⊑ ⊤`  (A person is a subclass of the universal class)  
- **Doctor**: A subclass of Person, representing medical professionals.  
  `Doctor ⊑ Person`  
- **Patient**: A subclass of Person, representing individuals receiving medical care.  
  `Patient ⊑ Person`  
- **Department**: Represents hospital departments.  
  `Department ⊑ ⊤`  
- **Treatment**: Represents procedures or medical services offered.  
  `Treatment ⊑ ⊤`  

---

### Roles (Relationships and Attributes)
#### Person Attributes:
- Each person has unique properties such as ID, name, age, address, contact number, and email.  
  ```
  Person ⊑ ∃hasPersonID.String  
  Person ⊑ ∃hasName.String  
  Person ⊑ ∃hasAge.Integer  
  Person ⊑ ∃hasAddress.String  
  Person ⊑ ∃hasContactNumber.String  
  Person ⊑ ∃hasEmail.String  
  ```

#### Doctor Attributes:
- Doctors have additional attributes like license ID, specialization, experience, schedule, and room number.  
  ```
  Doctor ⊑ ∃hasLicenseID.String  
  Doctor ⊑ ∃hasSpecialization.String  
  Doctor ⊑ ∃hasYearsOfExperience.Integer  
  Doctor ⊑ ∃hasSchedule.Schedule  
  Doctor ⊑ ∃hasRoomNumber.String  
  ```

#### Patient Attributes:
- Patients have illness details, insurance information, emergency contacts, admission, and discharge dates.  
  ```
  Patient ⊑ ∃hasIllness.String  
  Patient ⊑ ∃hasInsuranceProvider.String  
  Patient ⊑ ∃hasInsurancePolicyNumber.String  
  Patient ⊑ ∃hasEmergencyContact.String  
  Patient ⊑ ∃hasAdmissionDate.Date  
  Patient ⊑ ∃hasDischargeDate.Date  
  ```

#### Department Attributes:
- Departments have IDs, locations, head doctors, staff numbers, and operating hours.  
  ```
  Department ⊑ ∃hasDepartmentID.String  
  Department ⊑ ∃hasLocation.String  
  Department ⊑ ∃hasHeadOfDepartment.Doctor  
  Department ⊑ ∃hasNumberOfStaff.Integer  
  Department ⊑ ∃hasOperatingHours.String  
  ```

#### Treatment Attributes:
- Treatments have IDs, names, costs, durations, side effects, and medications.  
  ```
  Treatment ⊑ ∃hasTreatmentID.String  
  Treatment ⊑ ∃hasTreatmentName.String  
  Treatment ⊑ ∃hasCost.Double  
  Treatment ⊑ ∃hasDuration.Integer  
  Treatment ⊑ ∃hasSideEffects.String  
  Treatment ⊑ ∃hasMedicationsIncluded.List  
  ```

---

### Role Relationships with Cardinality Constraints
1. **Doctor Treats Patient**  
   ```
   Doctor ⊑ ∃treats.Patient  
   Cardinality: Doctor ⊑ ∀treats.(≥ 1 Patient)  
   Cardinality: Patient ⊑ ∀treatedBy.(≤ 1 Doctor)  
   ```

2. **Patient Receives Treatment**  
   ```
   Patient ⊑ ∃receivesTreatment.Treatment  
   Cardinality: Patient ⊑ ∀receivesTreatment.(≥ 1 Treatment)  
   Cardinality: Treatment ⊑ ∀appliedTo.(≥ 1 Patient)  
   ```

3. **Doctor Works In Department**  
   ```
   Doctor ⊑ ∃worksIn.Department  
   Cardinality: Doctor ⊑ ∀worksIn.(≤ 1 Department)  
   Cardinality: Department ⊑ ∀hasDoctors.(≥ 1 Doctor)  
   ```

4. **Department Head Is Doctor**  
   ```
   Department ⊑ ∃hasHeadOfDepartment.Doctor  
   Cardinality: Department ⊑ ∀hasHeadOfDepartment.(= 1 Doctor)  
   ```

---

## Section 3: Satisfiability Questions
### Q1: Can a Doctor also be a Patient?
- `Doctor ⊓ Patient ⊑ ⊥`  
- This implies that no individual can simultaneously be both a doctor and a patient.

### Q2: Can Every Doctor Be Required to Be a Head Doctor?
- `Department ⊑ ≤ 1 headOfDepartment.Doctor`  
- This restricts each department to having only one head doctor, preventing every doctor from being a head.

### Q3: Can a Patient Exist Without Treatment?
- `Patient ⊑ ≥ 1 receives.Treatment`  
- This mandates that every patient must have at least one treatment.

---

## Section 4: Implication Questions
### Q1: Emergency Treatment and Emergency Contact
- **Question**: Does receiving emergency treatment imply the patient has an emergency contact?  
  **Explanation**: Patients receiving emergency care should have emergency contacts on file.

### Q2: Doctor’s Specialization and Department
- **Question**: Does working in a department imply a doctor specializes in that field?  
  **Explanation**: Doctors are usually assigned based on their specialization.

### Q3: Multiple Treatments and Chronic Illness
- **Question**: Does receiving multiple treatments imply the patient has a chronic illness?  
  **Explanation**: Chronic illnesses often necessitate repeated treatments.

---

## Conclusion
This project models medical environments using Description Logic, focusing on class hierarchies, attributes, and relationships. It uses cardinality constraints and implication questions to simulate real-world medical scenarios, ensuring consistency in patient care and staff management.
