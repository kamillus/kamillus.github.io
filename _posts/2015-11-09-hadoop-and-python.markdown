---
layout: post
title:  "Using hadoop with python"
date:   2015-11-09 21:44:20
categories: hadoop, python, mapreduce
---
Hadoop is a powerful framework accomodating distributed processing through map/reduce jobs. Hadoop comes with Java api's, but how do you use it with python, ruby, or other languages? As it turns out, you can use other languages with Hadoop by utilizing piping (if you know unix piping, then this will seem familiar).

## Set up ##

First, let's upload a file to our HDFS. If our file is a text file named "students.txt" we would do:

	hadoop fs -put class/students.txt

The contents of the file look something like this and our goal is to calculate averages for each assignment:

	name	a1	80
	name	a2	40
	name	a3	20
	name2	a1	90
	name2	a2	80
	name3	a3	70

Next, we need to write 2 scripts.. one to perform a map, and another one to perform a reduce operation.

## Map ##

    from sys import stdin

    if __name__ == "__main__":
        for line in stdin:
            name, assignment, grade = line.strip().split("\t")
            print(assignment + "\t"+ grade)

## Reduce ##

    from sys import stdin

    if __name__ == "__main__":
    
        total = 0
        count = 0
    
        prev_assignment = ""
    
        for line in stdin:
            assignment, grade = line.strip().split("\t")
           
            total += int(grade)
            count += 1
        
            if assignment != prev_assignment:
                prev_assignment = assignment
                print(assignment + " average: \t"+ str(total/count))
                total = 0
                count = 0

## Execute ##

Now, we can run the following to execute our job:

	hadoop jar /path/to/hadoop-streaming.jar -mapper map.py -reducer reduce.py -file map.py -file reduce.py -input class -output result
	
Alternatively, use pipes to test your code:

	cat students.txt | python map.py | sort | python reduce.py