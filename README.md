- 👋 Hi, I’m @Saratreddi
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Saratreddi/Saratreddi is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

SELECT distinct pu.username USER_NAME,
Email_address
,papf.person_number EMPLOYEE_NUMBER
,ppn.first_name EMPLOYEE_FIRST_NAME
,ppn.last_name EMPLOYEE_LAST_NAME 
,DECODE(SUSPENDED,'Y', 'Inactive User','N', 'Active User') USER_STATUS
,ASSIGNMENT_STATUS_TYPE EMPLOYEE_STATUS
FROM PER_USERS pu 
,PER_PERSON_NAMES_F ppn,
 per_email_addresses PEA
,PER_ALL_PEOPLE_F papf 
,PER_ALL_ASSIGNMENTS_F paaf
WHERE pu.person_id = ppn.person_id 
AND pu.person_id = papf.person_id
AND paaf.person_id = papf.person_id 
AND TRUNC(SYSDATE) BETWEEN ppn.effective_start_Date AND ppn.effective_end_Date
AND TRUNC(SYSDATE) BETWEEN papf.effective_start_Date AND papf.effective_end_Date
AND TRUNC(SYSDATE) BETWEEN paaf.effective_start_Date AND paaf.effective_end_Date
AND name_type = 'GLOBAL'
and PEA.person_id(+)=papf.person_id
and pea.Email_type(+)='W1'
