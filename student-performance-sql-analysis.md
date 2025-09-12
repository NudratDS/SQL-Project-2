🔹 Question 1:

What is the average math, reading, and writing score overall and by gender?
-- Get overall average scores for math, reading, and writing
SELECT
  ROUND(AVG(math_score), 2) AS avg_math,
  ROUND(AVG(reading_score), 2) AS avg_reading,
  ROUND(AVG(writing_score), 2) AS avg_writing
FROM student_performance;

-- Get average scores grouped by gender
SELECT
  gender,
  ROUND(AVG(math_score), 2) AS avg_math,
  ROUND(AVG(reading_score), 2) AS avg_reading,
  ROUND(AVG(writing_score), 2) AS avg_writing
FROM student_performance
GROUP BY gender
ORDER BY gender;

***


🔹 Question 2:

How does parental level of education affect students’ average scores?
-- Compare average scores based on parental level of education
SELECT
  parental_education,
  ROUND(AVG(math_score), 2) AS avg_math,
  ROUND(AVG(reading_score), 2) AS avg_reading,
  ROUND(AVG(writing_score), 2) AS avg_writing,
  -- Calculate overall average of all three subjects
  ROUND((AVG(math_score) + AVG(reading_score) + AVG(writing_score)) / 3, 2) AS avg_overall
FROM student_performance
GROUP BY parental_education
ORDER BY avg_overall DESC;

***

🔹 Question 3:

What is the impact of completing the test preparation course on student scores?
-- Compare scores of students who completed or did not complete the test prep course
SELECT
  test_preparation_course,
  ROUND(AVG(math_score), 2) AS avg_math,
  ROUND(AVG(reading_score), 2) AS avg_reading,
  ROUND(AVG(writing_score), 2) AS avg_writing,
  -- Calculate average of total scores
  ROUND((AVG(math_score) + AVG(reading_score) + AVG(writing_score)) / 3, 2) AS avg_overall
FROM student_performance
GROUP BY test_preparation_course
ORDER BY avg_overall DESC;

***


🔹 Question 4:

Which combination of lunch type and gender yields the highest average total score?
-- Calculate average total score (math + reading + writing) grouped by gender and lunch type
SELECT
  gender,
  lunch,
  ROUND(AVG(math_score + reading_score + writing_score), 2) AS avg_total_score
FROM student_performance
GROUP BY gender, lunch
ORDER BY avg_total_score DESC
LIMIT 5;  -- Get top 5 combinations with highest average total score

***


🔹 Question 5:

Among students who did not complete the test preparation course, which parental education level group performs best? 
-- Filter students who did not complete the test prep course
-- Then group by parental education to find best-performing group
SELECT
  parental_education,
  ROUND(AVG(math_score), 2) AS avg_math,
  ROUND(AVG(reading_score), 2) AS avg_reading,
  ROUND(AVG(writing_score), 2) AS avg_writing,
  -- Calculate overall average of scores
  ROUND((AVG(math_score) + AVG(reading_score) + AVG(writing_score)) / 3, 2) AS avg_overall
FROM student_performance
WHERE test_preparation_course = 'none'  -- replace with actual value if different
GROUP BY parental_education
ORDER BY avg_overall DESC;
