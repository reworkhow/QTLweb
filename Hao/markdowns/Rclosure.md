# Advanced R -- Closures

****
## 1

For researchers familar with object oriented programming such as C++, closures in R should be an interesting part. Rohan told me about this way to code in R and already implemented it in his Rsim package simulating genotypic data in populations.

Basiclly, the concept of closures in R is similar to the concept of class in C++. Below is an example Rohan and I worked on together.



```

openAccount=function(name="Hao",deposit=0){

    myName = name
    balance=deposit

    putMoney=function(amount=0){
        balance<<-balance+amount    
        return(balance)
        }

    getMoney = function(amount=0){
        balance <<- balance-amount
        return (balance)
        }

    res=list(
        putMoney=putMoney,
        getMoney=getMoney,
        myName=myName,
        balance=balance
        )           

    return(res)   
 } 
```



~~Here an environment is built for **openAccount**, any call to functions or variables in the resturn list will modify the whole environment including myName,balance,get/putMoney. Let try it.~~



```
 > myAccount=openAccount(deposit=100)
 > myAccount$putMoney(15)
 [1] 115
 > myAccount$getMoney(50)
 [1] 65
 > myAccount$balance
 [1] 100

```



It seems to be wrong with the balance. It is never changed. Yes, it is wrong. This is a mistake Rohan and I made before. **list** cannot provide an environment( closure ). The reason why returned values from get/put balance keeps changing is the symbol **

****
## 2
A way to use R closure in this problem, which makes it possible to return the **balance**variable, is to waork with **new.env()**. Below is an example with R closure for the same problem.



```
openAccount = function(name="Hao",deposit=0){

    res = new.env()

    res$myName  = name
    res$balance = deposit

    res$putMoney = function(amount=0){ 
        res$balance <<- res$balance+amount
        return (res$balance)
        }

    res$getMoney = function(amount=0){
        res$balance <<- res$balance-amount
        return (res$balance)
        }

    return(res)
 }

```



Let's run it and see what we'll get.



```
 > myAccount=openAccount(deposit=100)
 > myAccount$putMoney(15)
 [1] 115
 > myAccount$getMoney(50)
 [1] 65
 > myAccount$balance
 [1] 65

```



Now everything is what I want. Here an environment for all members in this function is created. Now comes the last step.



```
 > myAccount$putMoney(1000000)
 [1] 1e+06
 > myAccount$balance
 [1] 1e+06

```



Haha, I'm rich now!!!


