# Cambridge Computer Science 15-Mark Solution
# Solved by Rayan Sajid
## Question (0478/21, Paper 2 – Algorithms, Programming and Logic, Oct/Nov 2025)

The scores for each competitor in an archery competition are recorded.  

- The one-dimensional array `competitorName[]` stores competitor names (max 30).  
- There are 10 rounds (max 30 per round), stored in 2D array `competitorScore[]`.  
- Highest and lowest score for each competitor are discarded.  
- Overall score = sum of remaining 8 scores.  
- Qualification rules:
  - 210 or more → moves on to next competition
  - 180–209 → reserve
  - below 180 → does not qualify  

**Requirements:**  
- Input scores for each competitor in each round  
- Validate input between 0–30  
- Calculate overall score (discard highest/lowest)  
- Output competitor name and classification  
- Output number of competitors in each category  

---

## Pseudocode Solution

```pseudocode
// Loop through all competitors
FOR i <-- 1 TO 30
    FOR j <-- 1 TO 10
        OUTPUT "Enter the score of ", CompetitorName[i], " for round ", j
        INPUT CompetitorScore[i,j]

        // Validate input score
        WHILE CompetitorScore[i,j] < 0 OR CompetitorScore[i,j] > 30
            OUTPUT "Please enter a value between 0 & 30 inclusive"
        ENDWHILE
    NEXT j

    // Sort scores in ascending order to remove highest and lowest
    FOR a <-- 1 TO 9
        FOR b <-- 1 TO 9
            IF CompetitorScore[i,b] < CompetitorScore[i,b+1] THEN
                T1 <-- CompetitorScore[i,b]
                CompetitorScore[i,b] <-- CompetitorScore[i,b+1]
                CompetitorScore[i,b+1] <-- T1
            ENDIF
        NEXT b
    NEXT a

    // Calculate overall score (sum of middle 8 scores)
    Total <-- 0
    FOR x <-- 2 TO 9
        Total <-- Total + CompetitorScore[i,x]
    NEXT x

    // Classify competitor
    IF Total >= 210 THEN
        Qualified <-- Qualified + 1
        Pos[i] <-- "Q"
    ELSE IF Total >= 180 THEN
        Reserve <-- Reserve + 1
        Pos[i] <-- "R"
    ELSE
        Fail <-- Fail + 1
        Pos[i] <-- "N"
    ENDIF
NEXT i

// Output each competitor’s result
FOR y <-- 1 TO 30
    OUTPUT CompetitorName[y]
    CASE OF Pos[y]
        Q: OUTPUT "Qualified"
        R: OUTPUT "Reserve"
        N: OUTPUT "Not Qualified"
    ENDCASE
NEXT y

// Output total numbers in each category
OUTPUT "Number of people who:"
OUTPUT "Qualified: ", Qualified
OUTPUT "Reserved: ", Reserve
OUTPUT "Not Qualified: ", Fail
