## prompt use bank

Given the contextual description of the target system, please generate an PlantUML representation of the target model based on the question.

Question:

```
Develop a UML class diagram with the structure of such a system, with all the elements mentioned above, the relationships between them, and all required integrity constraints, including the following:

- The values of all numeric data types must be correct (including, among others, that years and page numbers must be positive).
- No edition of a book may be earlier than its original edition.
- When the number of copies of any book, including all editions, exceeds 10,000, the book is considered a best-seller.
- A person cannot own more than 100 copies of the books he has authored.
```

Context:

```
We want to model a computerized system for book management, whose structure is described below.

- Each book has a title and one or more authors (e.g., Don Quixote, Miguel de Cervantes).
- In addition to the authors' names, their date of birth and death (if they are deceased) are also stored.
- Different editions of each book may exist, including the original one.
- An edition may be of one type (paperback, hardcover or deluxe), has a number of pages and is published in one year, by one publisher and in one language.
- Each edition may have a set of illustrators, who are in charge of the drawings of that edition (if any), as well as a set of translators, if the book has been translated from its original language.
- Publishers print a number of copies of each edition. Each copy has an owner, which can be the publisher itself (if no one has bought it yet -- this is the default option), a bookstore, a library, or an individual.

The behavior of the system allows books to be bought and borrowed.

- Libraries can lend books to their registered users or to other libraries.
- Individuals can only buy books through bookstores or from other individuals.
- However, libraries and stores can buy them from publishers directly, from other stores or from individuals.
- Publishers cannot buy books.
- Finally, individuals may sell books that they own, but not books that they have borrowed from a library.
- Libraries cannot sell books, only lend them, only if they own them and they are not borrowed.
- Stores may not borrow books from any library.
- Likewise, books may not be returned to a library that have not been previously borrowed.
```

Example is as follows：

Question:

```
Develop a UML class diagram with the structure of such a system, with all the elements mentioned above, the relationships between them, and all required integrity constraints.
```

 Context:

 ```
 Suppose the financial system of a country is composed of banks.

- Each bank has branches, which may be spread throughout the country, but there may not be more than three branches of the same bank in the same city.
- The structure of a bank's branches is hierarchical, so that a branch may have subordinate branches (of the same bank), either in the same city or in other cities.
- The customers of a branch can be either the individuals or companies that have an account at the branch. Each customer may have one or more accounts in any of the branches of a bank. Each account can have only one account holder, the customer who opens the account.
- Each branch owns an account, in which it stores its assets.
- Each account has a balance, which must be positive, unless it is a "credit" account.
- Credit accounts allow their balance to be negative, with a limit that is established when the account is opened.
- A customer may request a change in this limit from the branch where the account is held, and the branch must request authorization from the branch directly responsible for it (except the head office, at the root of the hierarchy, which can make decisions directly). Changes in the credit limit will be authorized as long as the new limit is lower than the previous one, or if it is only 10% higher than the one the account already had, and the current balance exceeds the new limit (e.g., if the credit limit is 1,000 Euros and you request to increase it to 1,005 Euros with a balance of 1,100 euros on the account, the branch will authorize the change).
- Customer can perform transactions with their accounts (request balance, deposit or withdraw money, and transfer money to another account). hey can also open accounts at any branch. When opening an account, the initial balance is 0. If the account is a credit account, the initial limit is 10 euros.
- The accounts have a maintenance fee of 1% per year. This means that, once a year (on January 1), each branch deducts 1% from the current balance of all its accounts. If the balance is 0 and the account is not a credit account, no money is deducted. In case of credit accounts, if the resulting balance is negative the branch will deduct 1% of the account's credit limit instead. The deducted money from the becomes the property of the branch and is stored in your account.
- All customers can transfer money from any of the accounts the own, to any other account -- no matter who the owner is, or the bank the destination account belongs to. Transfers between accounts of different banks have a 2% commission, i.e., if you transfer 1,000 euros, then 980 euros are deposited in the destination account. That 2% of the money becomes the property of the origin and destination branches (1% for each). Transfers between accounts of the same bank are free of charge.
- Companies with a balance of more than 1 million euros in one of their accounts are considered VIP by that bank and have a number of advantages. Firstly, in a transfer between banks, the part corresponding to the account of origin or destination that is of that bank is not taxed with the corresponding 1%. Secondly, these accounts do not pay an annual maintenance fee. Only companies, and not individuals, can be considered VIP.
- Finally, accounts whose holders are bank branches pay neither annual fee nor transfer commission in any bank.
 ```

Example target model:

 ```
 @startuml
' Classes
class Bank {
    + name: String
    + calculateInterbankCommission(): Float
}

class Branch {
    + id: String
    + city: String
    + assetsAccount: Account
    + calculateAnnualFee(account: Account): Float
    + authorizeCreditLimitChange(requestedLimit: Float, currentBalance: Float): Boolean
}

class Customer {
    + id: String
    + name: String
    + type: String <<enumeration>>  ' Individual or Company
    + isVIP(bank: Bank): Boolean
}

class Account {
    + id: String
    + balance: Float
    + type: String <<enumeration>>  ' Normal or Credit
    + creditLimit: Float
    + isCreditAccount(): Boolean
    + initializeCreditAccount(): Void
    + annualFee(): Float
    + transferFee(destinationBank: Bank, amount: Float): Float
}

class Transaction {
    + id: String
    + amount: Float
    + type: String <<enumeration>>  ' Deposit, Withdrawal, Transfer
    + commission: Float
    + execute(): Boolean
}

interface FeeRule {
    + calculateFee(account: Account): Float
}

' Relationships
Bank "1" -- "0..*" Branch : "has branches"
Branch "1" -- "0..*" Branch : "subordinate branches"
Branch "1" -- "0..*" Account : "owns"
Branch "1" -- "0..*" Customer : "serves"
Customer "1" -- "0..*" Account : "owns"
Account "1" -- "1" Customer : "belongs to"
Transaction "1" -- "1" Account : "affects"
Transaction "1" -- "1" Account : "originates from"
Account "1" ..|> FeeRule : "implements"

' Integrity Constraints
note left of Branch
"Max 3 branches of the same bank in a city"
end note

note left of Account
"Credit accounts allow negative balance within limit"
"Initial credit limit = 10"
"Special accounts (branch-owned) exempted from fees"
end note

note left of Customer
"VIP if balance > 1 million"
"Only Companies can be VIP"
end note

note left of Transaction
"Inter-bank transfers: 2% commission"
"Intra-bank transfers: Free"
"Commissions split between origin and destination branch"
end note
@enduml
 ```

## book prompt

Question:

```
Develop a UML class diagram with the structure of such a system, with all the elements mentioned above, the relationships between them, and all required integrity constraints, including the following:

- The values of all numeric data types must be correct (including, among others, that years and page numbers must be positive).
- No edition of a book may be earlier than its original edition.
- When the number of copies of any book, including all editions, exceeds 10,000, the book is considered a best-seller.
- A person cannot own more than 100 copies of the books he has authored.
```

Context:

```
We want to model a computerized system for book management, whose structure is described below.

- Each book has a title and one or more authors (e.g., Don Quixote, Miguel de Cervantes).
- In addition to the authors' names, their date of birth and death (if they are deceased) are also stored.
- Different editions of each book may exist, including the original one.
- An edition may be of one type (paperback, hardcover or deluxe), has a number of pages and is published in one year, by one publisher and in one language.
- Each edition may have a set of illustrators, who are in charge of the drawings of that edition (if any), as well as a set of translators, if the book has been translated from its original language.
- Publishers print a number of copies of each edition. Each copy has an owner, which can be the publisher itself (if no one has bought it yet -- this is the default option), a bookstore, a library, or an individual.

The behavior of the system allows books to be bought and borrowed.

- Libraries can lend books to their registered users or to other libraries.
- Individuals can only buy books through bookstores or from other individuals.
- However, libraries and stores can buy them from publishers directly, from other stores or from individuals.
- Publishers cannot buy books.
- Finally, individuals may sell books that they own, but not books that they have borrowed from a library.
- Libraries cannot sell books, only lend them, only if they own them and they are not borrowed.
- Stores may not borrow books from any library.
- Likewise, books may not be returned to a library that have not been previously borrowed.

```

## DistributionCompanies Prompt

Question:

```
Develop a UML class diagram with the structure of such a system, with all the elements mentioned above, the relationships between them, and all required integrity constraints.
```

Context:

```
We want to model the structure and behavior of a set of distribution companies.

- Each company has a number of employees, including a director, a manager, and at least one base worker.
- All employees have a salary. Of course, a person can work in several companies (though never in more than three), and therefore have different salaries.
- Within the same company, the director has to be paid more than the manager, and the manager more than the base workers.
- In addition, a person cannot hold two positions in the same company, i.e., a director cannot be a manager or a base worker, a manager cannot be a director or a base worker, and base workers cannot be managers or directors of that company (although they can be in other companies).
- Each company sells a series of products (e.g., screws, long bits, short bits, nails, hammers, etc.), each with its own price. Of course, the price of items of the same product must be the same within the same company, but it may vary between different companies selling the same product.
- People who place orders with a company become its customers.
- Each order includes a number of items of the products sold by the company (for example, an order may be for 10 nails and 2 hammers, or for three chairs and two tables).
- Each order must exceed a minimum value, otherwise it is not profitable for the company. Each company defines the minimum value of its orders.
- Each company has two types of customers: normal customers, which are those who have placed at least one order, and VIP customers, which are those who have placed orders totaling more than 1,000 Euros. As soon as a customer becomes a VIP, he gets a 10% discount on all new orders. Let us further assume that the employees of a company are considered VIPs as soon as they start working for the company.
- Companies have a set of items in stock in their warehouse at any given time. No one can place an order for items that are not in the company's warehouse.
- Once an order is placed, the item disappears from the company's warehouse and becomes the property of the person who placed the order.
- Finally, the same person cannot have items of more than 10 different product types, regardless of the company where they were purchased.

The behavior of the system is determined by a set of actions that allow:

- Purchasing items by placing orders,
- Replenishing the companies' warehouses, and
- Hiring and firing companies' workers.
```

## JavaMetaModel

Context:

```
We want to develop a metamodel for a basic subset of the Java programming language.
```

Questions:

```
Develop a UML class diagram with the abstract syntax of a subset of the Java programming language to allow the definition of classes, their attributes and methods. More specifically, it must be able to represent at least the following concepts: Basic Type (int, byte, short, long, float, double, boolean and char), Class, Attribute, Method and Parameter (of a method). Attributes, methods and parameters must have a name and a type, which can be a basic type or a previously defined class. It must also be possible to describe the cardinality and visibility (public, protected, default or private) of the language elements. Finally, it must be possible to define inheritance relationships between classes. Include all required integrity constraints.
```
