Knuth–Morris–Pratt algorithm

the Knuth–Morris–Pratt string searching algorithm (or KMP algorithm) searches for occurrences of a "word" W within a main "text string" S 
by employing the observation that when a mismatch occurs, the word itself embodies sufficient information to determine where the next match 
could begin, thus bypassing re-examination of previously matched characters.The algorithm was conceived in 1970 by Donald Knuth and Vaughan 
Pratt, and independently by James H. Morris. The three published it jointly in 1977.



To illustrate the algorithm's details, consider a (relatively artificial) run of the algorithm, where W = "ABCDABD" and S = "ABC ABCDAB ABCDABCDABDE". At any given time, the algorithm is in a state determined by two integers:

    m, denoting the position within S where the prospective match for W begins,
    i, denoting the index of the currently considered character in W.

In each step the algorithm compares S[m+i] with W[i] and advances i if they are equal. This is depicted, at the start of the run, like

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W: ABCDABD
i: 0123456

The algorithm compares successive characters of W to "parallel" characters of S, moving from one to the next by incrementing i if they match. However, in the fourth step S[3] = ' ' does not match W[3] = 'D'. Rather than beginning to search again at S[1], we note that no 'A' occurs between positions 1 and 2 in W; hence, having checked all those characters previously (and knowing they matched the corresponding characters in S), there is no chance of finding the beginning of a match. Therefore, the algorithm sets m = 3 and i = 0.

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W:    ABCDABD
i:    0123456

This match fails at the initial character, so the algorithm sets m = 4 and i = 0

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W:     ABCDABD
i:     0123456

Here i increments through a nearly complete match "ABCDAB" until i = 6 giving a mismatch at W[6] and S[10]. However, just prior to the end of the current partial match, there was that substring "AB" that could be the beginning of a new match, so the algorithm must take this into consideration. As these characters match the two characters prior to the current position, those characters need not be checked again; the algorithm sets m = 8 (the start of the initial prefix) and i = 2 (signaling the first two characters match) and continues matching. Thus the algorithm not only omits previously matched characters of S (the "BCD"), but also previously matched characters of W (the prefix "AB").

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W:         ABCDABD
i:         0123456

This search fails immediately, however, as W does not contain another "A", so as in the first trial, the algorithm returns to the beginning of W and begins searching at the mismatched character position of S: m = 10, reset i = 0.

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W:           ABCDABD
i:           0123456

The match at m=10 fails immediately, so the algorithm next tries m = 11 and i = 0.

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W:            ABCDABD
i:            0123456

Once again, the algorithm matches "ABCDAB", but the next character, 'C', does not match the final character 'D' of the word W. Reasoning as before, the algorithm sets m = 15, to start at the two-character string "AB" leading up to the current position, set i = 2, and continue matching from the current position.

             1         2  
m: 01234567890123456789012
S: ABC ABCDAB ABCDABCDABDE
W:                ABCDABD
i:                0123456
