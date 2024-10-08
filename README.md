# 1.Map Reduce program to read a text file count the number of occurrences of the words.

# 1. mapper.py

- mapper.py

```py
#!/usr/bin/env python
import sys
for line in sys.stdin:
    line = line.strip()
    words = line.split()
    for word in words:
        print '%s\t%s' % (word, 1)

```

# 1. reducer.py

- reducer.py

```py
#!/usr/bin/env python
from operator import itemgetter
import sys
current_word = None
current_count = 0
word = None
for line in sys.stdin:
    line = line.strip()
    word, count = line.split('\t', 1)
    try:
        count = int(count)
    except ValueError:
        continue
    if current_word == word:
        current_count += count
    else:
        if current_word:
            print '%s\t%s' % (current_word, current_count)
        current_count = count
        current_word = word
if current_word == word:
    print '%s\t%s' % (current_word, current_count)

```
# 
# 2: Map Reduce program to display the number of transactions and sales count from shopping cart.

- shopping.txt

```bash
2012-07-16     15:43	 Bangalore	Men's Clothing	208.97	Visa	
2012-07-18     20:15	 Mumbai  	Electronics	1005.20	cash
```

# 2. mapper.py

```py
#!/usr/bin/env python
import string
import fileinput
for line in fileinput.input():
    data = line.strip().split("\t")
    if len(data) == 6:
        date, time, location, item, cost, payment = data
        print "{0}\t{1}".format(location, cost)
```

# 2. reducer.py

```py
#!/usr/bin/env python
import fileinput
transactions_count = 0
sales_total = 0
for line in fileinput.input():
    data = line.strip().split("\t")    
    if len(data) != 2:
        continue
    current_key, current_value = data
    transactions_count += 1
    sales_total += float(current_value)
print transactions_count, "\t", sales_total

```
# 
# 3: Map Reduce program to calculate the average age for each gender.

- t3.csv

```bash
0001,1,21,72,180,3,1
0002,2,33,62,110,1,2
0003,1,43,52,80,1,2
0004,2,23,83,90,1,2
```

# 3. mapper.py

```py
#!/usr/bin/python
import sys
for line in sys.stdin:
    line = line.strip()
    line = line.split(",")
    if len(line) >=2:
        gender = line[1]
        age = line[2]
        print '%s\t%s' % (gender, age)
```

# 3. reducer.py
```py
#!/usr/bin/python
import sys
gender_age = {}
for line in sys.stdin:
    line = line.strip()
    gender, age = line.split('\t')
    if gender in gender_age:
        gender_age[gender].append(int(age))
    else:
        gender_age[gender] = []
        gender_age[gender].append(int(age))
for gender in gender_age.keys():
    ave_age = sum(gender_age[gender])*1.0 / len(gender_age[gender])
    print '%s\t%s'% (gender, ave_age)
```

#
# 4. TERMWORK4

- data.csv
```bash
1,M,25000,2,Agree
2,F,50000,1,Disagree
3,M,75000,0,Neutral
4,F,80000,2,Agree
5,F,10000,1,DisAgree
6,F,20000,3,Neutral
7,M,17000,0,DisAgree
8,F,15000,0,DisAgree
9,M,60000,1,Agree
10,F,45000,1,Agree
11,F,46000,3,DisAgree
12,F,50000,3,Neutral
```

# 4. mapper.py

```py
#!/usr/bin/env python
import sys
for line in sys.stdin:
    line = line.strip()
    line = line.split(",")
    if len(line) >=2:
        pid = line[0]
        opinion = line[4]
        print '%s\t%s' % (pid, opinion)
```

# 4. reducer.py

```py
#!/usr/bin/env python
import sys
opiniondic={}
count=0
for line in sys.stdin:
    line = line.strip()
    pid, opinion = line.split('\t')
    if opinion in opiniondic:
        opiniondic[opinion].append(count+1)
    else:
        opiniondic[opinion] = []
        opiniondic[opinion].append(count+1)
for op in opiniondic.keys():
    count=len(opiniondic[op])
    print '%s\t%s'% (op,count)
```


# 5. TERMWORK5

- t5.csv
```bash
E001, Sunita, Accounts, 15000 
E002, Harsh, IT, 50000
E003, Ragini, IT, 75000
E004, Mithun, Accounts, 20000 
E005, Pruthavi, Marketing, 45000
E006, Anjali, IT, 70000
E007, Kunal, Marketing, 60000
E008, Mitali, Accounts, 55000
E009, Roopa, IT, 70000
E010, Deepti, Accounts, 30000 
E011, Janavi, Marketing, 25000
E012, Lata, Accounts, 30000 
E013, Brijmohan, Marketing, 45000
E014, Nina, Accounts, 50000
E015, Pallavi, Marketing, 25000
```

# 5. mapper.py

```py
#!/usr/bin/env python
import sys
for line in sys.stdin:
    line = line.strip()
    line = line.split(",")
    if len(line) >=2:
        dept = line[2]
        sal = line[3]
        print '%s\t%s' % (dept, sal)
```

# 5. reducer.py

```py
#!/usr/bin/env python
import sys
deptdic={}


for line in sys.stdin:
    line = line.strip()
    dept,sal = line.split('\t')
    if dept in deptdic:
        deptdic[dept].append(int(sal))
    else:
        deptdic[dept] = []
        deptdic[dept].append(int(sal))
for dept in deptdic.keys():
    sum_sal = sum(deptdic[dept])
    print '%s\t%s'% (dept,sum_sal)
```
