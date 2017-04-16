# A-game
import random
import string
from time import sleep

error=0
total=0
ttgame=0

hun=random.randint(100,999)
one=random.randint(2,9)
two=random.randint(2,9)
ten=one+two*10
ttt=one*hun
qqq=two*hun
kkk=hun*ten
alist=[]
def makenumber(hun,ten,one,two,alist):
        hun=random.randint(100,999)
        one=random.randint(2,9)
        two=random.randint(2,9)
        ten=one+two*10
        ttt=one*hun
        qqq=two*hun
        kkk=hun*ten
        while 1:
            if (one==two or two*hun<1000 or one*hun<1000):
                hun=random.randint(100,999)
                one=random.randint(2,9)
                two=random.randint(2,9)
                ten=one+two*10
                ttt=one*hun
                qqq=two*hun
                kkk=hun*ten
            else:
                alist=[hun,ten,two,one,ttt,qqq,kkk]
                return alist
                break
alist = makenumber(hun,ten,one,two,alist)
thelist=[alist[0],alist[1]]
hun=alist[0]
ten=alist[1]
one=alist[3]
two=alist[2]
ttt=alist[4]
qqq=alist[5]
kkk=alist[6]
print (thelist,hun,ten,one,two,ttt,qqq,kkk)

string1='ABCDEFGHIJ'
def randomcypher(string1):
        varlist=list(string1)
        random.shuffle(varlist)
        dshuffle=dict(enumerate(varlist))
        return dshuffle
dshuffle=randomcypher(string1)
print(dshuffle)

def encrypting(formstring):
        result=''
        for letter in formstring:
                result+=dshuffle[int(letter)]
        return result
formstring='%3s%2s%4s%4s%5s'%(hun,ten,ttt,qqq,kkk)
stastring='%s%s'%(error,ttgame)
encrypting(formstring)
formstring=encrypting(formstring)
puzzle='  '+formstring[:3]+'      Number of errors (this game):\nx  '+formstring[3:5]+'\n-----\n '+formstring[5:9]+'      Number of games:\n'+formstring[9:13]+'\n-----\n'+formstring[13:]+'      Average number of errors per game:\n\n\n'
print('\n\n  ',formstring[:3],'      Number of errors (this game):',error,'\nx  ',formstring[3:5],'\n-----\n ',formstring[5:9],'      Number of games:',ttgame,'\n',formstring[9:13]+'\n-----\n'+formstring[13:]+'        Average number of errors per game:\n\n\n')

thetry=' '
def interactive(dshuffle,formstring):
        global error

        youtry=input( "Your try? ")
        uyoutry=youtry.capitalize()
        while not(uyoutry in list(dshuffle.values())):
            print("That is not a code value.")
            youtry=input( "Your try? ")

        thetry=input("%s="%(uyoutry))
        if int(thetry)>=0 and int(thetry<=9) and (int(thetry)in dshuffle):
                if(dshuffle[int(thetry)]==uyoutry):
                        print("Correct!")
                        formstring=formstring.replace(uyoutry,thetry)
                        del dshuffle[int(thetry)]
                        sleep(2)
                else:
                        print("Incorrect!")
                        error+=1
        else:
                print("That is not a hidden value.")
                sleep(2)
        return formstring
                            
interactive(dshuffle,formstring)
while 1:
        makenumber(hun,ten,one,two,alist)
        randomcypher(string1)
        while 1:
                encrypting(formstring)
                result=encrypting(formstring)
                if result == True:
                        break
                else:
                        interactive(dshuffle)
        print("Finish with",error,"errors")
        total = total+error
        ttgame+=1
        
