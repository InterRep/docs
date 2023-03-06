# Twitter

## Parameters

-   **Followers**: number of followers of the user;
-   **Botometer overall score**: "Complete Automation Probability" score (`cap`) calculated by [Botometer](https://botometer.iuni.iu.edu/#!/) (a tool for measuring the probability that a Twitter account is run by a bot).
-   **Verified profile**: whether the user has a verified profile.

## Levels
|                         followers                         |    < 100    |     < 1k      |    < 10k    |  < 100k  |  +100k   |
|:---------------------------------------------------------:|:-----------:|:-------------:|:-----------:|:--------:|:--------:|
|          is likely bot (botometer `cap` >= 0.95)          |  commoner   |   commoner    |  commoner   | commoner | commoner |
| is likely not bot (botometer `cap` < 0.95) & not verified |  commoner   | up-and-coming | established |   star   |   icon   |
| is likely not bot (botometer `cap` < 0.95) & not verified |  commoner   | up-and-coming | established |   star   |   icon   |
|   is likely not bot (botometer `cap` < 0.95) & verified   | established |  established  | established |   star   |   icon   |
