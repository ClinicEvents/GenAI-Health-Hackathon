# Challenge 16: Radiological entities recognition


The aim is to use LLM tools and various techniques like Retrieval-Augmented Generation (RAG) to identify Snowmed terminology contained in anonymized clinical register documents.

## Objective

Extraction of radiological reports and generation of loinc codes for each document.


## AWS Tools
- Bedrock
- S3

## Database
 
-	BASE16: Dataset SAP Clinical Pain 
-	OUT16 (Write-only backup where the challenge results will be stored).

## Data Preparation Process

- Data extraction: The data is based on CARMEN-I's anonimized corpus.
- The dataset is divided in two groups: training and testing.
- The LLM will recieve the training group as an input to learn the data and then it will recieve the test group to predict the correct tag. The prediction quality will be measured.
- Anonimization: CARMEN-I's data is already anonimized.

## Evaluation metrics

The used metrics ara:
-	**Accuracy:** Measures the correct predictions percentage from the total of the model predictiones.
-	**Sensibility:** Also known as recall or True Positive Rate, it measures the model's capacity to identify the positive instances.
-	**Specifity:** Also known as True Negative Rate, it measures the model's capacity to identify the negative instances.
-	**F1 score:** It is the precision and sensibility harmonic median. Provides a balance between both metrics and is useful when the false positives and negatives are wanted to be equilibrated.

