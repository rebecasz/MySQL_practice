https://www.hackerrank.com/challenges

hackers table : 

hacker_id integer
name string

difficulty table : 

difficulty_level integer
score integer

challenges table :

challenge_id integer
hacker_id integer
difficulty_level integer

submissions table:

submission_id integer
hacker_id integer
challenge_id integer
score integer

### 1. Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

SELECT
    h.hacker_id,
    h.name
FROM
    hackers h
    JOIN submissions s ON h.hacker_id = s.hacker_id
    JOIN challenges c ON s.challenge_id = c.challenge_id
    JOIN difficulty d ON c.difficulty_level = d.difficulty_level AND s.score = d.score
GROUP BY
    h.hacker_id, h.name
HAVING
    COUNT(DISTINCT s.challenge_id) > 1
ORDER BY
    COUNT(DISTINCT s.challenge_id) DESC,
    h.hacker_id ASC;


