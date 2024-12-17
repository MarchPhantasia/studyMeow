## bank

``` 
@startuml
!theme mars
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

## book

```
@startuml
' Classes
class Book {
    + title: String
    + isBestSeller(): Boolean
}

class Author {
    + name: String
    + dateOfBirth: Date
    + dateOfDeath: Date
    + calculateOwnershipLimit(): Boolean
}

class Edition {
    + type: String <<enumeration>>  ' Paperback, Hardcover, Deluxe
    + numberOfPages: PositiveInteger
    + publicationYear: PositiveInteger
    + isOriginalEdition(): Boolean
}

class Publisher {
    + name: String
    + publishCopies(edition: Edition, count: PositiveInteger): Void
}

class Copy {
    + owner: String <<enumeration>>  ' Publisher, Bookstore, Library, Individual
}

class Illustrator {
    + name: String
}

class Translator {
    + name: String
}

class Library {
    + lendBook(copy: Copy, to: LibraryOrUser): Boolean
    + returnBook(copy: Copy): Boolean
}

class Store {
    + sellBook(copy: Copy, to: Individual): Boolean
}

class Individual {
    + name: String
    + sellBook(copy: Copy, to: Individual): Boolean
    + buyBook(copy: Copy, from: StoreOrIndividual): Boolean
}

' Relationships
Book "1" -- "1..*" Author : "written by"
Book "1" -- "1..*" Edition : "has editions"
Edition "1" -- "0..*" Copy : "is represented by"
Edition "1" -- "0..*" Illustrator : "illustrated by"
Edition "1" -- "0..*" Translator : "translated by"
Edition "1" -- "1" Publisher : "published by"
Copy "1" -- "1" Owner : "owned by"
Library "1" -- "0..*" Copy : "owns"
Store "1" -- "0..*" Copy : "sells"
Individual "1" -- "0..*" Copy : "owns"

' Integrity Constraints
note left of Book
"Best-seller if copies exceed 10,000"
end note

note left of Edition
"Years and page numbers must be positive"
"No edition earlier than original"
end note

note left of Author
"Cannot own more than 100 copies of authored books"
end note

note left of Library
"Lend books only if owned and not borrowed"
"Books must be returned to the same library"
end note

note left of Store
"Cannot borrow books from libraries"
end note

note left of Individual
"Cannot sell borrowed books"
"Can only buy from stores or other individuals"
end note

@enduml
```

## DistributionCompanies

``` 
@startuml
' Classes
class Book {
    + title: String
    + isBestSeller(): Boolean
}

class Author {
    + name: String
    + dateOfBirth: Date
    + dateOfDeath: Date
    + calculateOwnershipLimit(): Boolean
}

class Edition {
    + type: String <<enumeration>>  ' Paperback, Hardcover, Deluxe
    + numberOfPages: PositiveInteger
    + publicationYear: PositiveInteger
    + isOriginalEdition(): Boolean
}

class Publisher {
    + name: String
    + publishCopies(edition: Edition, count: PositiveInteger): Void
}

class Copy {
    + owner: String <<enumeration>>  ' Publisher, Bookstore, Library, Individual
}

class Illustrator {
    + name: String
}

class Translator {
    + name: String
}

class Library {
    + lendBook(copy: Copy, to: LibraryOrUser): Boolean
    + returnBook(copy: Copy): Boolean
}

class Store {
    + sellBook(copy: Copy, to: Individual): Boolean
}

class Individual {
    + name: String
    + sellBook(copy: Copy, to: Individual): Boolean
    + buyBook(copy: Copy, from: StoreOrIndividual): Boolean
}

' Relationships
Book "1" -- "1..*" Author : "written by"
Book "1" -- "1..*" Edition : "has editions"
Edition "1" -- "0..*" Copy : "is represented by"
Edition "1" -- "0..*" Illustrator : "illustrated by"
Edition "1" -- "0..*" Translator : "translated by"
Edition "1" -- "1" Publisher : "published by"
Copy "1" -- "1" Owner : "owned by"
Library "1" -- "0..*" Copy : "owns"
Store "1" -- "0..*" Copy : "sells"
Individual "1" -- "0..*" Copy : "owns"

' Integrity Constraints
note left of Book
"Best-seller if copies exceed 10,000"
end note

note left of Edition
"Years and page numbers must be positive"
"No edition earlier than original"
end note

note left of Author
"Cannot own more than 100 copies of authored books"
end note

note left of Library
"Lend books only if owned and not borrowed"
"Books must be returned to the same library"
end note

note left of Store
"Cannot borrow books from libraries"
end note

note left of Individual
"Cannot sell borrowed books"
"Can only buy from stores or other individuals"
end note

@enduml
```

## JavaMetaModel

```
@startuml
' Classes
class JavaModel {
    + classes: Set<Class>
}

class Class {
    + name: String
    + visibility: Visibility <<enumeration>> ' public, protected, default, private
    + attributes: Set<Attribute>
    + methods: Set<Method>
    + inheritsFrom: Class [0.]
}

class Attribute {
    + name: String
    + type: Type
    + visibility: Visibility
    + cardinality: String <<format>> 'e.g., 1, 0..*, 1..n'
}

class Method {
    + name: String
    + returnType: Type
    + visibility: Visibility
    + parameters: List<Parameter>
}

class Parameter {
    + name: String
    + type: Type
}

abstract class Type {
    + name: String
}

class BasicType extends Type {
    + predefinedTypes: List<String> = ['int', 'byte', 'short', 'long', 'float', 'double', 'boolean', 'char']
}

class UserDefinedType extends Type {
    + refClass: Class
}

' Relationships
JavaModel "1" -- "0..*" Class : "contains"
Class "0..*" -- "0..*" Attribute : "has"
Class "0..*" -- "0..*" Method : "has"
Method "0..*" -- "0..*" Parameter : "takes"
Attribute "1" -- "1" Type : "of type"
Parameter "1" -- "1" Type : "of type"
Class "1" --|> Type : "is a"
BasicType "0..*" --|> Type : "is a"

' Integrity Constraints
note left of Class
"Classes can inherit from one other class"
"Class names must be unique"
end note

note left of Attribute
"Attributes must have unique names within a class"
"Cardinality must follow Java syntax rules"
end note

note left of Method
"Method names must be unique within a class"
"Return type can be a basic type or user-defined type"
end note

note left of Parameter
"Parameter names must be unique within a method"
end note

note left of BasicType
"Basic types are predefined as int, byte, short, long, float, double, boolean, char"
end note

@enduml
```
