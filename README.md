You are to implement another class that can replace NaiveEngine. Your class must implement GuessEngine, but it must do much better guesses. every guess the program does should have the property that it can not be ruled out because of the user's existing responses. In principle it is easy to describe how to do this: the list codes should contain only codes that can be the secret, given the answers already received by the user.
+
+You should start by carefully reading through NaiveEngine and determining which parts you can keep unchanged and what you need to improve. A lot can be reused! Note also that none of the other classes from the zip file needs to be changed.
+
+The main improvement is thus to reduce codes so that it only contains possible secrets. Prior to the first guess codes consists of all possible codes: you have not yet received any response. Each call of answerNewGuess to the model knows how right/wrong the latest guess was. One can then go through the list of codes and remove any element which does not give exactly the same response to the last guess.
+
+For each possible secret from the list of codes you should determine whether it leads to the answer reply for the guess newGuess. This in turn requires that the program can figure out what the reply should be for the guess newGuess given a specific the secret. If we do this then it is enough to compare the reply given from the user with the reply computed for a potential secret from the list codes. If they do not match then the corresponding code is removed.
+
+to calculate the answer for given secret and guess
+
+We recommend you to define a function that takes two codes secret and guess as parameters and returns a Reply. The response that the user should gives if the secret is secret and the guess is guess. It may seem strange that one could make use of this feature: When can you use it in program?; You do not know what the secret is?
+
+We repeat the above idea: you have to take the time necessary to understand how it is supposed to work. After each guess codes will only contain the secrets that have not yet been ruled out. We choose one of these randomly as the next guess and we get the user's response. If this answer is not four bulls (in which case we guessed the secret) then we do the following. We consider in a sequence each remaining element in codes as a possible secret and we use our function to calculate the response that the user should give in this case, and we compare with the response that we got. If these are not the same then assumption wrong, so secret can not be the secret and can be removed from codes.
+
+One way to define this function is the following:
+
+  
+the number of bulls is easy to calculate by a loop walking through secret and guess in parallel and counting the number of times the colors are equal.   
+We can calculate the sum of the number of bulls and cows as follows:   
+For each color col calculate the number of times that color appears in both secret and in guess. The minimum of these two numbers is the sum of the number of bulls and cows of color col. Summation over all colors gives the total number of bulls and cows.   
+
+We can calculate the number of cows by substracting the number of bulls.
+We also strongly recommend you to write a small test program to test it on so that you are sure that the function is working properly. Then you use it in the filtration of codes in answerNewGuess.
+
+When you have come so far, you can replace NaiveEngine with your model class and test the program. If the user provides correct answers the program will normally find the secret within six guesses. If the user gives the wrong answer for some guess you will eventually be in a situation where codes is empty, i.e. there are no new guesses to do. Then You can not do anything but throw an exception. To pass the lab you do not need to improve explainContradiction from NaiveEngine, i.e. you don't need to identify the user's mistake.
