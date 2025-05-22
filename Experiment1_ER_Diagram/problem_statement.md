# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.
---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Student Name

## Scenario Chosen:
Hospital 

## ER Diagram:
![image](https://github.com/user-attachments/assets/e8b65991-719d-4440-b539-0af374606d5e)

## Entities and Attributes:
- Patient: (PatientID,FullName,DOB,Gender,Address,PhoneNumber,Email,InsuranceDetails)
- Doctor: (DoctorID,FullName,Specialization,PhoneNumber,Email,WorkSchedule)
- Department: (DepartmentID,DepartmentName,DepartmentHead)
- Appointment: (AppointmentID,AppointmentDate,AppointmentTime,ReasonForVisit)
- MedicalRecord: (MedicalRecordID,Diagnosis,PrescribedMedications,Treatments,TestResults,OtherMedicalInfo)
- Billing: (BillID,TotalAmount,BillingDate,PaymentStatus)
- Payment: (PaymentID,PaymentDate,PaymentMethod,AmountPaid)

## Relationships and Constraints:
-Enrolls: A patient enrolls in many appointments; each appointment is linked to exactly one patient (1:M), with total participation on patient side and partial on 
- appointment side.
- Conducts: A doctor conducts many appointments; each appointment is linked to exactly one doctor (1:M), with partial participation on doctor and appointment sides.
- BelongsTo: A doctor belongs to exactly one department; one department can have many doctors (1:M), with total participation for doctor and partial for department.
- Generates: Each appointment generates exactly one medical record; each medical record is linked to exactly one appointment (1:1), with total participation on both sides.
- BilledBy: Each appointment is billed by one bill (1:1), with total participation on both sides.
- PaidBy: One bill is paid by multiple payments; each payment is linked to exactly one bill (1:M), with total participation on both sides.
## Extension:
- Billing is modeled as a separate entity linked 1:1 with Appointment to capture charges for each visit.
- Payment is modeled as a separate entity linked 1:M with Billing to support multiple payments per bill, allowing for partial or mixed payment methods.
- 
## Design Choices:
- Entities were chosen to capture critical patient management data: patients, doctors, departments, appointments, medical records, billing, and payments.
- Relationships are designed to efficiently link patients, doctors, appointments, and billing information.
- Billing and Payment are separated to allow detailed tracking of payment status and methods.
- Total participation is enforced where necessary (e.g., every patient must have at least one appointment, every doctor must belong to a department).
- Partial participation is used where the relationship may be optional (e.g., doctors may have no appointments at a given time).
## RESULT
The concepts of ER modeling is applied by creating an ER diagram for real-world application.
