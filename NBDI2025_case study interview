-- using LOWER() to clean and standardise data. 

WITH cleaned AS (
  SELECT
    company
    ,CASE
      WHEN LOWER(department) LIKE '%execut%' THEN 'Executive'
      WHEN LOWER(department) LIKE '%board%' THEN 'Board'
      ELSE NULL
    END AS role
    ,position
    ,educational_background
    ,gender
    ,nationality
    ,year_of_Birth
  FROM `cosmic-axe-464811-t3.Casestudyinterview.NBDI2025`
)

-- Only keep Executive
,executive_only AS (
  SELECT *
  FROM cleaned
  WHERE role = 'Executive'
)

-- gender standardisation 
,gender_clean AS (
  SELECT
    *
    ,CASE
      WHEN LOWER(gender) IN ('m', 'male') THEN 'Male'
      WHEN LOWER(gender) IN ('f', 'female') THEN 'Female'
      ELSE 'Other/Unknown'
    END AS gender_std
  FROM executive_only
)

-- educational background standardisation
,edu_clean AS (
  SELECT
    company
    ,gender_std
    ,position
    ,nationality
    ,year_of_birth
    ,CASE
      WHEN educational_background IS NULL OR TRIM(educational_background) = '' THEN 'N/A'
      WHEN LOWER(educational_background) LIKE '%business%' 
        OR LOWER(educational_background) LIKE '%economics%' 
        OR LOWER(educational_background) LIKE '%finance%' 
        THEN 'Business'
      WHEN LOWER(educational_background) LIKE '%law%' 
        OR LOWER(educational_background) LIKE '%legal%' 
        THEN 'Law'
      WHEN LOWER(educational_background) LIKE '%engineer%' 
        THEN 'Engineering'
      WHEN LOWER(educational_background) LIKE '%science%' 
        OR LOWER(educational_background) LIKE '%biology%' 
        OR LOWER(educational_background) LIKE '%chemistry%' 
        OR LOWER(educational_background) LIKE '%physics%' 
        THEN 'Sciences'
      WHEN LOWER(educational_background) LIKE '%history%' 
        OR LOWER(educational_background) LIKE '%philosophy%' 
        OR LOWER(educational_background) LIKE '%literature%' 
        THEN 'Humanities'
      WHEN LOWER(educational_background) LIKE '%medicine%' 
        OR LOWER(educational_background) LIKE '%medical%' 
        THEN 'Medicine'
      WHEN LOWER(educational_background) LIKE '%art%' 
        OR LOWER(educational_background) LIKE '%design%' 
        THEN 'Arts'
      ELSE CONCAT('Other: ', educational_background)
    END AS education_std
  FROM gender_clean
)

-- Count the number of people by field of education in each company
,edu_counts AS (
  SELECT
    company
    ,education_std
    ,COUNT(*) AS n_by_field
  FROM edu_clean
  GROUP BY company, education_std
)

-- calculation 
,summary AS (
  SELECT
    company
    ,SUM(n_by_field) AS number_executive
    ,COUNT(DISTINCT education_std) AS number_unique_edu
    ,ROUND(MAX(n_by_field) / SUM(n_by_field), 2) AS share_top_field
    ,ROUND(1 - MAX(n_by_field) / SUM(n_by_field), 2) AS diversity_score
  FROM edu_counts
  GROUP BY company
)

SELECT *
FROM summary
ORDER BY diversity_score DESC;
