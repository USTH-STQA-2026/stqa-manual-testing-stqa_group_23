Cross-Checking Report: Group 23 evaluating Group 08
1. General Overview
Group 23 has reviewed the four manual testing documents from Group 08: Test Cases, Test Execution, Bug Reports, and Test Summary Report. Overall, Group 08 did a really solid and careful job. The documents are well-organized and follow the system requirements clearly.

2. What Group 08 Did Well

Good Test Design: The group correctly used testing techniques like Equivalence Partitioning and Boundary Value Analysis. We highly appreciate their use of a Decision Table for the "Borrow Book" function. It was a smart way to cover all the complex conditions without writing too many repetitive test cases.

Clear Bug Reports: The bug reports are very easy to understand. Instead of writing many small bugs for the same feature, they grouped them well by root cause. They also found a very serious privacy bug, where users can actually see other people's borrow history.

Solid Test Summary: The summary report is short but provides all the necessary information, like their 75% Pass Rate. They prioritized the most important bugs correctly and made a logical conclusion that the system is not ready to be released.

3. Areas for Improvement

Confusing "Due Date" Logic: There is a conflict about the dueDate = currentDate rule across their documents. In the Test Cases, returning a book exactly on the due date is considered "Overdue". However, in the Test Execution, the exact same situation is marked as "Blocked" because the group noted that the system does not see it as overdue. Group 08 needs to make sure this logic is consistent in all files.

Long Test Steps: In some test cases, the test steps ask the tester to manually borrow books many times. It would be much faster to just write "The account already reached the maximum borrow limit" in the Preconditions to save testing time.

4. Simple Comparison: Group 23 vs Group 08

What our group did better: We wrote a larger amount of test cases and covered more specific scenarios across all the functions. Our Pass Rate is also slightly higher.

What their group did better: Group 08 has much better document consistency. Their Bug IDs match perfectly between the Test Execution and Bug Reports files without any confusion. Also, they did a better job at grouping bugs by the main root cause, whereas we split similar bugs into separate reports.

5. Conclusion
Group 08 submitted a very good manual testing project. Except for a minor logical mistake regarding the due date, the rest of the work shows strong effort and serious teamwork. overall score 17/20

6. link
Group23: https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_23
Group08: https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_08