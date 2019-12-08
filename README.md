# 8hwfinal
# HW 8  Final Alyson Shirley
# Instructions: Write a program which gives the user a menu of files and the user selects a text file.
# The program creates a dictionary which counts how many times each word is used (case-insensitive, so "hello" and "Hello" and "HeLLo" are the same word).
# It then creates a printed list of the top 25 words used and their relative frequencies (percentages, not raw counts).
# The program should correctly handle incorrect input from the user.


import os
import re


### READ FILE
def readfile(fyle):
    L = []
    s = open(fyle, "r")
    while True:
        line = s.readline()
        # print (line)
        if not line:
            break
        else:
            L.append(line)
    return L


### PICK FILE
def pickFile():
    phyle_name = ""

    dir_list = os.listdir()
    print("Enter the file to analyze?")
    reply = input(">")

    if reply in dir_list:
        phyle_name = reply;
    else:
        valid_selected = False
        while not valid_selected:
            i = 0
            print("File not found - please select one of these by number")
            for item in dir_list:
                print(i, " - ", item)
                i += 1
            reply = input(">")
            if int(reply) < i:
                phyle_name = dir_list[int(reply)]
                valid_selected = True

    print("Processing ", phyle_name)
    phyle_contents = readfile(phyle_name)
    # print( phyle_contents )
    phyle_dict = data2dict(phyle_contents)
    analyseFreq(phyle_dict)
    return


### DATA TO DICT
def data2dict(L):
    d = dict()
    words = ""
    for line in L:
        line = line.strip()
        print(line)
        line = line.lower()
        print(line)
        words = line.split(" ")
        print(words)

        for word in words:
            if word in d:
                d[word] += 1
            else:
                d[word] = 1

    print(d)
    # for key in list(d.keys()):
    # print(key, ":", d[key])


### SORT DICT -- can't get this to work but here is an attempt at counting the frequency of values from the 0 to 24 indicies
''' def sortDict(d):
   lst = list(d.items())
   print(lst).head(24)
   from collections import Counter
   sort_list=[lst]
   counts = Counter(list1)
   print(counts)'''


### FREQUENCY
def analyseFreq(lst):
    analyze_list = [lst]
    print("The original list is : " + str(analyze_list))


### MAIN
def main():
    still_analyzing = True
    while still_analyzing:
        pickFile()

        # check to stop or analyze another file
        print("Do you want to analyze another file (Y/N)?")
        reply = input(">")
        if reply.upper() == "N":
            still_analyzing = False
            print("Exit")


if __name__ == '__main__':
    main()
