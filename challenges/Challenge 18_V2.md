# Challenge 18: AI-guided Virtual Medical Simulation (MediRol)


Virtual clinical case simulator based on console-style RPG games
The simulator will guide the doctor through a story (simulation), where the user must indicate the various actions they wish to take to complete the case. The case will change with the iterations depending on the user's actions, which will allow the final outcome of the case to be modified.
This system is an example of learning through gamification, where various clinical cases will be collected to be solved. The idea is that the AI will collect data from prefabricated and normalized clinical cases in an open format, so the community can autonomously create new cases after the model is developed.
A specific format will also be created for the structuring of these cases, designed for the LLM to process them in the most efficient way possible. Additionally, the creation of clinical cases by doctors will be automated using the LLM itself, which will also serve as a double-check to ensure the correct creation of the cases.



## Objective

Create an AI-guided medical simulator that collects data from prefabricated and normalized clinical cases in an open format, allowing the autonomous creation of new cases after the model's development.

## Expected Outcomes

1.	**Incorporation of Real-Time Feedback:** Add a real-time feedback system that provides the user with hints or explanations about the consequences of their decisions during the simulation. This could include visualizations of the impact of clinical decisions on the patient's evolution.
2.	**User Ranking and Competitions:** Implement a points or ranking system that evaluates the effectiveness and speed with which users solve clinical cases. This will foster friendly competition and motivate users to improve their skills.
3.	**Improvement of LLM Hallucination:** Enhance the model's algorithms to avoid generating incorrect information during the simulation of clinical decisions. A peer review system or manual review of AI-generated cases could be implemented.
4.	**Inclusion of Multidisciplinary Simulations:** Allow the inclusion of multiple clinical specialties in the cases (e.g., a surgeon, intensivist, and radiologist) so that users can see how decisions in one area affect others. This would better reflect the real environment in a hospital.
5.	**Validation with Real Data:** Use real anonymized patient data to validate the accuracy of the simulator. The results obtained by the AI in the simulation will be compared with real-life clinical outcomes.
6.	**Incorporation of Predictive Models:** Include predictive algorithms that anticipate the likely outcome of the user's decisions based on large volumes of historical data. For example, predicting the patient’s survival rate based on the decisions made.
7.	**Open API for Creating New Cases:** Develop an open API to allow clinicians to upload their own cases and share them with the community. The API would integrate automated validations to ensure the consistency and quality of new cases.
8.	**Evaluation of Ethical Decision-Making:** Add scenarios that evaluate not only the user’s clinical expertise but also their ethical decision-making (e.g., in situations of resource scarcity or informed consent).
9.	**Real-Time Simulations with Multidisciplinary Teams:** Allow multiple users to participate simultaneously in the simulation from different clinical roles, fostering collaboration in decision-making.

   

## Tools

Participants will have the following information/tools to complete the challenge.

- Database:
    - Information about the database.

- Develop:
    - Jupyter Notebook
    - Bedrock
    - Shared bucket 

- Guides. It is recommended to consult the following demos:
    - DEMO_bedrock_connection
    - DEMO_RAG_with_KnowledgeBase
    - DEMO_RAG_with_Kendra
    - DEMO_download_studies_and_upload_to_s3
    - DEMO_s3_read_file
    - DEMO_s3_write_file

**NOTE:** If a patient is not found in the databases, the k-anonimization has deleted it.


**All development must be carried out using the services available on AWS. Moving information outside of the specified tools is NOT allowed.**

Below are details of the most relevant aspects of the tools available to participants.

 ### Database
 [BASE18](https://us-west-2.console.aws.amazon.com/s3/buckets/data-clinic-hackathon-2024?region=us-west-2&bucketType=general&prefix=BASE18/&showversions=false). Your mentor will provide you with more details about the information that contains this database.





### Shared bucket

Participants have access to a shared bucket to store any necessary documents for the challenge.

```
https://us-west-2.console.aws.amazon.com/s3/buckets/shared-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects
```

Each group has access ONLY to the folder named after their group. It is recommended to check the demos `DEMO_s3_read_file` and `DEMO_s3_write_file` to learn how to read and write files from a bucket. Use the following values in the demos:

```python
BUCKET_NAME = 'shared-clinic-hackathon-2024'
BUCKET_FILE_LOCATION_AND_NAME = '<grupo_name>/<file_name>'
# NOTE:
# - replace <grupo_name> by the name of your team  (e.g. Team1)
# - replace <file_name> by the file name you want to read/write.
```

## Results

The challenge will only be considered valid if participants save ALL files necessary to reproduce the solution proposed by the group members. This implies that if the group members modified any provided files or used external information to solve the challenge, these must be included as part of the solution.

Files must be saved in the bucket: [results-clinic-hackathon-2024](https://us-west-2.console.aws.amazon.com/s3/buckets/results-clinic-hackathon-2024?region=us-west-2&bucketType=general&tab=objects). The file location within the bucket (prefixes) must be: `<group_name>/<challenge_name>/<file_name>`.

It is recommended to use the `DEMO_s3_write_file` demo to write the files/code of the proposed solution. Use the following values in the demos:

```python
BUCKET_NAME = 'results-clinic-hackathon-2024'
BUCKET_FILE_LOCATION_AND_NAME = '<group_name>/<challenge_name>/<file_name>'
# NOTA: :
# - replace <group_name> by the name of your team (e.g. Team1)
# - replace <challenge_name>  by the name of the challenge (e.g. Challenge1)
# - replace <file_name> by the name of the file that you want to store (e.g., main_code_challenge1.ipynb)

```

## Evaluation Metrics

1.	**ROUGE (Recall-Oriented Understudy for Gisting Evaluation):** Primarily used to evaluate automatic text summaries by comparing them with a set of reference summaries.
2.	**Predictive Evaluation Based on Real Data:** Real anonymized clinical data will be used to validate the simulator’s results. The accuracy of the simulator's predictions will be assessed against the actual outcomes of the patients.
3.	**Standardized User Performance Evaluation System:** A system will be developed to evaluate the performance of users interacting with the LLM, using indicators such as the number of iterations completed, ineffective iterations, and the time taken to solve the case.
4.	**Participant Satisfaction:** The satisfaction generated by the tool among clinical participants will be evaluated on-site, as well as the tool's overall performance.
5.	**Hallucination Evaluation:** The adequacy of the generated document will be assessed, along with any erroneous hallucination generated during the simulation. This ensures the data and guides are as accurate as posible
6.	**Study of social biases:** The performance of the LLM should be evaluated when generating the simulations as well as when creating a document to simulate. It should be studied if there is any racial or social bias when creating the clinical case xml as well as when representing the data in the simulation, comparing this method with other case creation methods using LLMs.The performance of the LLM should be evaluated when generating the simulations as well as when creating a document to simulate. It should be studied if there is any racial or social bias when creating the clinical case xml as well as when representing the data in the simulation, comparing this method with other case creation methods using LLMs.




