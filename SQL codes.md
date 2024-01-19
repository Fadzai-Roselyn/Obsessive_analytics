## SQL
## Loading data in to pgAdmin4 and creating tables
CREATE TABLE OCDdataset (
  PatientID INTEGER,
  Age INTEGER,
  Gender VARCHAR,
  Ethnicity VARCHAR,
  MaritalStatus VARCHAR,
  EducationLevel VARCHAR,
  OCDDiagnosisDate DATE,
  DurationOfSymptoms INTEGER,
  PreviousDiagnoses VARCHAR,
  FamilyHistoryOfOCD VARCHAR,
  ObsessionType VARCHAR,
  CompulsionType VARCHAR,
  YBOCSScoreObsessions INTEGER,
  YBOCSScoreCompulsions INTEGER,
  DepressionDiagnosis VARCHAR,
  AnxietyDiagnosis VARCHAR,
  Medications VARCHAR

)

COPY OCDdataset(PatientID, Age, Gender, Ethnicity, MaritalStatus, EducationLevel, OCDDiagnosisDate, DurationOfSymptoms, PreviousDiagnoses, FamilyHistoryOfOCD, ObsessionType, CompulsionType, YBOCSScoreObsessions,YBOCSScoreCompulsions,DepressionDiagnosis, AnxietyDiagnosis, Medications)
FROM 'C:\Program Files\PostgreSQL\16\ocd_patient_dataset.csv'
DELIMITER ','
CSV HEADER;

SELECT * 
from
	ocddataset

### Count of female vs male patients and averag of the Y-BOCS score respectively
SELECT
    Gender,
    count("patientid") AS num_patients,
    round(avg("ybocsscoreobsessions")::numeric, 2) AS avg_obs_score
FROM
	public.ocddataset
    
GROUP BY
    Gender;

### Result
![Alt text](image.png)

### Number of patients by ethnicity and respective Y-BOCS Score; obsession
SELECT
    ethnicity,
    count(patientid) AS num_patients,
    round(avg(ybocsscoreobsessions)::numeric, 2) AS obs_score
FROM
    public.ocddataset
GROUP BY
    ethnicity
ORDER BY
    num_patients;

### Result
![Alt text](image-1.png)

### Obsession types and respective patient count and obsession Y-BOCS Scores
SELECT
  obsessiontype,
  count(DISTINCT patientid) AS num_patients,
  round(avg(ybocsscoreobsessions), 2) AS obs_score
FROM
  public.ocddataset
GROUP BY
  obsessiontype
ORDER BY
  num_patients desc;

### Result
![Alt text](image-2.png)

### Compulsion types and respective patient count and compulsion Y-BOCS Scores
SELECT
  compulsiontype,
  count(DISTINCT patientid) AS num_patients,
  round(avg(ybocsscorecompulsions), 2) AS obs_score
FROM
  public.ocddataset
GROUP BY
  compulsiontype
ORDER BY
  num_patients desc;

### Result
  ![Alt text](image-3.png)

