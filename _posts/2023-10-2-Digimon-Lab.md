---
layout: post
title: Digimon Lab
author: Ellen Wang
gh-repo: ellenwang105/art-of-data
gh-badge: [star, fork, follow]
tags: [test]
comments: true
---

**Author:** Ellen Wang

**Collaborators:** Izzy Fic, Emma Chang, Feingold (No code was shared, but we were able to talk through ideas for certain problems and ask for insight when we could not figure out why an error was showing up)

![Digimon](https://upload.wikimedia.org/wikipedia/en/4/43/Digimon_Digital_Monsters_Season_1_DVD_Cover.png)

https://en.wikipedia.org/wiki/Digimon_Adventure_%281999_TV_series%29

In this lab, I used the csv library and the DictReader() function (https://docs.python.org/3/library/csv.html) to create a reader for the csv file, where each dictionary in the reader contained all of the information for one digimon and allowed me to iterate through the information. 

## Finding the Average Speed

For me, this task felt very intuitive. First, I thought about how an average is calculated, which is by adding up all values and dividing by the number of values. Then, I iterated through the csv file by using a "for" loop. For every dictionary in the reader, I appended the value corresponding to the key "Spd" to a list that contained all of the speeds of each digimon. Lastly, I added up all the values in the list, and divided by the total length, which gave me the average speed.

## Finding the number of Digimon with a certain attribute

For this task, I created a function that took in two parameters: one that would be the type of attribute that we were looking for (ex. "Type"), and another that was the specific attribute (ex. "Vaccine"). Then, I created a variable that represented the number of digimon that had a specific attribute of that type. Next, I iterated through all of the dictionaries in the reader, and if the value of the key was equal to the specific attribute we were looking for, 1 was added to the number of digimon with that attribute.

## Finding an optimal team

When I first read the task, I didn't have a clear way that I wanted to approach the problem. I had a few ideas that I wanted to try, but I was totally sure which would be the most efficient.

My initial instinct was to iterate through the reader 3 times using nested for loops, checking every time if the digimon combination would work. But I quickly realized that this was highly inefficient, and I was also having trouble breaking the loop at the right time.

Next, I had an idea of picking two random Digimon, and finding a third one that would meet the memory and attack requirements when added onto a team with the first two. This was actually the approach that took me the most amount of time, and I think I was quite close to making it work in the end. Here was the code that I wrote:

~~~
def choose_digi():
    with open("datasets/digimon.csv", "r") as f:
        reader = csv.DictReader(f)
    
        digi1 = random.randint(1,249) #Change to length
        digi2 = random.randint(1,249)
        
        name_team(digi1,digi2)

def name_team():
    
    with open("datasets/digimon.csv", "r") as f:
        reader = csv.DictReader(f)
    
        total_memory = 0
        total_atk = 0
        
        
        team_digi = []
        for row in reader:
            if float(row["Number"]) == player1 or float(row["Number"]) == player2:
                team_digi.append(row)
    
        #print(team_digi)
        
        for i in team_digi:
            total_memory += float(i["Memory"])
            total_atk += float(i["Atk"])
        
        if total_memory >= 15:
            team_digi = []
            choose_digi()
        
    with open("datasets/digimon.csv", "r") as f:
        reader = csv.DictReader(f)
                        
        for row in reader:
            if total_memory + float(row["Memory"]) <= 15 and total_atk + float(row["Atk"]) >= 300:
                team_digi.append(row)
                break
            
        if len(team_digi) == 2:
            choose_digi()
            
        final_memory = 0
        final_atk = 0
        for i in team_digi:
            final_memory += float(i["Memory"])
            final_atk += float(i["Atk"])
        
    print(team_digi)
    print("This team of Digimon has a total memory of " + str(final_memory) + " and a total attack of " + str(final_atk))
~~~

My idea was to first call the choose_digi function, which would randomly select two digimon out of the full list. Then, the name_team function would check whether those first two digimon met the attack and memory requirements, and if they didn't, the choose_digi function would need to be recalled again to generate two new random digimon. Afterwards, the computer would iterate through the reader, looking for a third digimon that would make the attack exceed 300 while keeping the memory below 15.

This code actually did work sometimes -- however, it would break whenever I ran the code twice in a row, and sometimes it would not even find a third digimon that would satisfy the requirements. I spent a lot of time trying to make this work, but in the end I resorted to a simpler method.

The code that I ended up going with is, unfortunately, not universally applicable, but works for this specific task. Because we are looking for a team of up to 3 digimon, I programmed the code so that the team would have exactly 3 members. Because the maximum memory is 15 and the minimum attack is 300, I iterated through the reader, picking out all of the digimon that had a memory less than or equal to 5, and an attack greater than or equal to 100, and appending them to a list. Once I had that list, I simply chose the first three in the list and assigned them as my team. 

## Other Takeaways and Learnings

Through this lab, I also was able to explore more about opening files and using dictionaries. One persistent problem that I kept running into was how to restart iteration at the beginning of the csv file, or the reader. I was originally using the seek() function to bring the position back to the start of the file; however, this did not work because seek() bases positions off of characters, not rows or keys. Thus, I was having a hard time converting strings into floats and finding the correct key-value pairs.

Then, I tried to create a function that would use a "with" statement to open the csv file, and call that whenever I wanted to reset. However, because of indentation, I could not call this function within another function successfully without the file being closed. In the end, I decided to just copy and paste the same "with" statement whenever I needed it and coding whatever I needed within the "with" statement (with proper indentation).

Overall, this was a very fun lab, and I'm curious to know if there is a better way of solving the team problem!
