1) What Are Regular Expressions?

• You use regular expressions to search for (and manipulate) simple and complex patterns in string data by using standard syntax conventions.

• You use a set of SQL functions and conditions to search for and manipulate strings in SQL and PL/SQL.

• You specify a regular expression by using:

– Metacharacters, which are operators that specify the search algorithms

– Literals, which are the characters for which you are searching

2) Benefits of Using Regular Expressions

Regular expressions enable you to implement complex match logic in the database with the following benefits:

• By centralizing match logic in Oracle Database, you avoid intensive string processing of SQL results sets by middle-tier applications.

• Using server-side regular expressions to enforce constraints, you eliminate the need to code data validation logic on the client.

• The built-in SQL and PL/SQL regular expression functions and conditions make string manipulations more powerful and easier than in previous releases of Oracle Database 10g.

3) Using the Regular Expressions Functions and Conditions in SQL and PL/SQL

• REGEXP_LIKE :- Similar to the LIKE operator, but performs regular expression matching instead of simple pattern matching (condition).

• REGEXP_REPLACE :- Searches for a regular expression pattern and replaces it with a replacement string.

• REGEXP_INSTR :- Searches a string for a regular expression pattern and returns the position where the match is found.

• REGEXP_SUBSTR :- Searches for a regular expression pattern within a given string and extracts the matched substring.

• REGEXP_COUNT :- Returns the number of times a pattern match is found in an input sting.

4) What Are Metacharacters

• Metacharacters are special characters that have a special meaning such as a wildcard, a repeating character, a nonmatching character, or a range of characters.

• You can use several predefined metacharacter symbols in the pattern matching.

• For example, the ^(f|ht)tps?:$ regular expression searches for the following from the beginning of the string:

– The literals f or ht

– The t literal

– The p literal, optionally followed by the s literal

– The colon “:” literal at the end of the string

5) Using Metacharacters with Regular Expressions

^ :- Matches the beginning of a string

$ :- Matches the end of a string

\ :- Treats the subsequent metacharacter in the expression as a literal

\n :- Matches the nth (1–9) preceding subexpression of whatever is grouped within parentheses. The parentheses cause an expression to be remembered; a backreference refers to it.

\d :- A digit character

[:class:] :- Matches any character belonging to the specified POSIX character class

[^:class:] :- Matches any single character not in the list within the brackets

6) Using the REGEXP_LIKE Condition

REGEXP_LIKE(source_char, pattern [, match_parameter ])

SELECT first_name, last_name FROM employees WHERE REGEXP_LIKE (first_name, '^Ste(v|ph)en$');

7) Using the REGEXP_REPLACE Function

REGEXP_REPLACE(source_char, pattern [,replacestr [, position [, occurrence [, match_option]]]])

SELECT REGEXP_REPLACE(phone_number, ‘\.',‘-') AS phone FROM employees;

8) Using the REGEXP_INSTR Function

REGEXP_INSTR (source_char, pattern [, position [,occurrence [, return_option [, match_option]]]])

SELECT street_address,REGEXP_INSTR(street_address,'[[:alpha:]]') AS First_Alpha_Position FROM locations;

9) Using the REGEXP_SUBSTR Function

REGEXP_SUBSTR (source_char, pattern [, position [, occurrence [, match_option]]])

SELECT REGEXP_SUBSTR(street_address , ' [^ ]+ ') AS Road FROM locations;

10) Subexpressions

• You may need to find a specific subpattern that identifies a protein needed for immunity in mouse DNA.

SELECT REGEXP_INST('ccacctttccctccactcctcacgttctcacctgtaaagcgtccctccctcatccccatgcccccttaccctgcagggtagagtaggctagaaaccagagagctccaagctccatctgtggagaggtgccatccttgggctgcagagagaggagaatttgccccaaagctgcctgcagagcttcaccacccttagtctcacaaagccttgagttcatagcatttcttgagttttcaccctgcccagcaggacactgcagcacccaaagggcttcccaggagtagggttgccctcaagaggctcttgggtctgatggccacatcctggaattgttttcaagttgatggtcacagccctgaggcatgtaggggcgtggggatgcgctctgctctgctctcctctcctgaacccctgaaccctctggctaccccagagcacttagagccag','(gtc(tcac)(aaag))',1, 1, 0, 'i',1) "Position" FROM dual;

11) Using the REGEXP_COUNT Function

REGEXP_COUNT (source_char, pattern [, position [, occurrence [, match_option]]])

SELECT REGEXP_COUNT('ccacctttccctccactcctcacgttctcacctgtaaagcgtccctccctcatccccatgcccccttaccctgcagggtagagtaggctagaaaccagagagctccaagctccatctgtggagaggtgccatccttgggctgcagagagaggagaatttgccccaaagctgcctgcagagcttcaccacccttagtctcacaaagccttgagttcatagcatttcttgagttttcaccctgcccagcaggacactgcagcacccaaagggcttcccaggagtagggttgccctcaagaggctcttgggtctgatggccacatcctggaattgttttcaagttgatggtcacagccctgaggcatgtaggggcgtgggatgcgctctgctctgctctcctctcctgaacccctgaaccctctggctaccccagagcacttagagccag‘,‘gtc’) AS Count FROM dual;

12) Regular Expressions and Check Constraints: Examples

ALTER TABLE emp8 ADD CONSTRAINT email_addr CHECK(REGEXP_LIKE(email,'@')) NOVALIDATE;

INSERT INTO emp8 VALUES (500,'Christian','Patel','ChrisP2creme.com', 1234567890,'12-Jan-2004','HR_REP',2000,null,102,40);

References:

Oracle® Database Reference 11g Release 1 (11.1)

Oracle® Database SQL Language Reference 11g Release 1 (11.1)

Oracle® Database Concepts 11g Release 1 (11.1)

Oracle® University examples
