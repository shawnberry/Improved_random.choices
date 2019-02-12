# Improved_random.choices
# I have improved Python 3's built-in function random.choices() from O(N**2) to O(N)





# Compare Shawn's code without random.choices() on lines 14-35 to the same much slower code with random.choices() on lines 37-59.
from datetime import datetime
import random

for k in range(3, 5):
    
    time0 = datetime.today()
    N = 10 ** k
    dictTimestamp = dict(); events = ['A', 'B', 'C', 'D', 'E',]; weights = [2, 2, 1, 1, 1]; total_weight = sum(weights)
    for i in range(1, N+1):
        r = random.random()    
        for j in range(len(events)):
            if sum(weights[:j])/total_weight <= r < sum(weights[:j+1])/total_weight:
                dictTimestamp[i] = events[j]
                
    countA, countB, countC, countD, countE = 0, 0, 0, 0, 0 
    for v in dictTimestamp.values():
        if v == 'A': countA += 1
        elif v == 'B': countB += 1
        elif v == 'C': countC += 1
        elif v == 'D': countD += 1
        elif v == 'E': countE += 1
    
    print('* Generate dataset where events A and B each occur twice as frequently as events C, D, or E.')
    print('Distribution where A, B each occur at 2/7 frequency (' + str(round(2*N/7)), 'times) and C, D, E each occur at 1/7 frequency (' + str(round(N/7)), 'times).\nA occured:', countA, '\nB occured:', countB, '\nC occurred:', countC, '\nD occurred:', countD, '\nE occurred:', countE)
      
    time1 = datetime.today()
    print('The elapsed time for this program with Shawn\'s code and N =', N, 'was', time1 - time0)
    
    time2 = datetime.today()
    print()
    
    dictTimestamp = dict()
    for i in range(1,N+1):
        dictTimestamp[i] = random.choices(['A', 'B', 'C', 'D', 'E',], [2/7, 2/7, 1/7, 1/7, 1/7,], k=N+1)[i]
    countA, countB, countC, countD, countE = 0, 0, 0, 0, 0 
    for v in dictTimestamp.values():
        if v == 'A':
            countA += 1
        elif v == 'B':
            countB += 1
        elif v == 'C':
            countC += 1
        elif v == 'D':
            countD += 1
        elif v == 'E':
            countE += 1
    print('* Generate dataset where events A and B each occur twice as frequently as events C, D, or E.')
    print('Distribution where A, B each occur at 2/7 frequency (' + str(round(2*N/7)), 'times) and C, D, E each occur at 1/7 frequency (' + str(round(N/7)), 'times).\nA occured:', countA, '\nB occured:', countB, '\nC occurred:', countC, '\nD occurred:', countD, '\nE occurred:', countE)
            
    time3 = datetime.today()
    print('The elapsed time for this program with random.choices() and N =', N, 'was', time3 - time2, 'which is', round((time3 - time2)/(time1 - time0), 2), 'times longer than Shawn\'s method')
    
    if k == 3:
        print('\n-------------------------------------------------------------------\n')
    
