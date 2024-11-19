## 一、实验目的

1. 大语言模型 ChatGPT 能否生成 MagicDraw 中 XMI 类型的模型？
2. 上下文学习中的案例提示是否有用？
3. ChatGPT 生成的效果怎么样？

## 二、实验设置

### 2.1 角色指定

### 2.1 角色指定

```
You are an expert in the field of systems engineering, please proceed with the follow-up work
```

### 2.2 带有案例的 prompt

```
Given the contextual description of the target system, please generate an XMI representation of the target model based on the question.
Question:
    '''
Develop a Sysml Block Definition Diagram with the structure of such a system, with all the elements mentioned above, the relationships between them, and all required integrity constraints.
    '''
Context:
    '''
Suppose the financial system of a country is composed of banks.

Each bank has branches, which may be spread throughout the country, but there may not be more than three branches of the same bank in the same city.
The structure of a bank's branches is hierarchical, so that a branch may have subordinate branches (of the same bank), either in the same city or in other cities.
The customers of a branch can be either the individuals or companies that have an account at the branch. Each customer may have one or more accounts in any of the branches of a bank. Each account can have only one account holder, the customer who opens the account.
Each branch owns an account, in which it stores its assets.
Each account has a balance, which must be positive, unless it is a "credit" account.
Credit accounts allow their balance to be negative, with a limit that is established when the account is opened.
A customer may request a change in this limit from the branch where the account is held, and the branch must request authorization from the branch directly responsible for it (except the head office, at the root of the hierarchy, which can make decisions directly). Changes in the credit limit will be authorized as long as the new limit is lower than the previous one, or if it is only 10% higher than the one the account already had, and the current balance exceeds the new limit (e.g., if the credit limit is 1,000 Euros and you request to increase it to 1,005 Euros with a balance of 1,100 euros on the account, the branch will authorize the change).
Customer can perform transactions with their accounts (request balance, deposit or withdraw money, and transfer money to another account). hey can also open accounts at any branch. When opening an account, the initial balance is 0. If the account is a credit account, the initial limit is 10 euros.
The accounts have a maintenance fee of 1% per year. This means that, once a year (on January 1), each branch deducts 1% from the current balance of all its accounts. If the balance is 0 and the account is not a credit account, no money is deducted. In case of credit accounts, if the resulting balance is negative the branch will deduct 1% of the account's credit limit instead. The deducted money from the becomes the property of the branch and is stored in your account.
All customers can transfer money from any of the accounts the own, to any other account -- no matter who the owner is, or the bank the destination account belongs to. Transfers between accounts of different banks have a 2% commission, i.e., if you transfer 1,000 euros, then 980 euros are deposited in the destination account. That 2% of the money becomes the property of the origin and destination branches (1% for each). Transfers between accounts of the same bank are free of charge.
Companies with a balance of more than 1 million euros in one of their accounts are considered VIP by that bank and have a number of advantages. Firstly, in a transfer between banks, the part corresponding to the account of origin or destination that is of that bank is not taxed with the corresponding 1%. Secondly, these accounts do not pay an annual maintenance fee. Only companies, and not individuals, can be considered VIP.
Finally, accounts whose holders are bank branches pay neither annual fee nor transfer commission in any bank.
    '''

Example is as follows：
Question:
    '''
Develop a Sysml Block Definition Diagram with the structure of such a system, with all the elements mentioned above
    '''
Context:
    ```
We want to model a computerized system for book management, whose structure is described below.

Each book has a title and one or more authors (e.g., Don Quixote, Miguel de Cervantes).
In addition to the authors' names, their date of birth and death (if they are deceased) are also stored.
Different editions of each book may exist, including the original one.
An edition may be of one type (paperback, hardcover or deluxe), has a number of pages and is published in one year, by one publisher and in one language.
Each edition may have a set of illustrators, who are in charge of the drawings of that edition (if any), as well as a set of translators, if the book has been translated from its original language.
Publishers print a number of copies of each edition. Each copy has an owner, which can be the publisher itself (if no one has bought it yet -- this is the default option), a bookstore, a library, or an individual.
The behavior of the system allows books to be bought and borrowed.

Libraries can lend books to their registered users or to other libraries.
Individuals can only buy books through bookstores or from other individuals.
However, libraries and stores can buy them from publishers directly, from other stores or from individuals.
Publishers cannot buy books.
Finally, individuals may sell books that they own, but not books that they have borrowed from a library.
Libraries cannot sell books, only lend them, only if they own them and they are not borrowed.
Stores may not borrow books from any library.
Likewise, books may not be returned to a library that have not been previously borrowed.
    ```
Example target model:
    ```
    <uml:Model xmi:type="uml:Model" xmi:id="eee_1045467100313_135436_1" name="Model">
      <ownedComment xmi:type="uml:Comment" xmi:id="_2022x_2fe013d_1729499324105_865173_3095"
                    body="Author:ASUS.&#xA;Created:10/1/12 3:10 PM.&#xA;Title:.&#xA;Comment:.&#xA;">
         <annotatedElement xmi:idref="eee_1045467100313_135436_1"/>
      </ownedComment>
      <packagedElement xmi:type="uml:Package" xmi:id="_2022x_2fe013d_1729584613781_486404_2819"
                       name="Books">
         <packagedElement xmi:type="uml:Class" xmi:id="_2022x_2fe013d_1729584640093_901664_2857"
                          name="Book">
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584709779_210599_3021"
                            name="title"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.String"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584716902_338465_3023"
                            name="year"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Integer"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584894285_695564_3070"
                            name="edition"
                            visibility="public"
                            type="_2022x_2fe013d_1729584643451_951576_2892"
                            association="_2022x_2fe013d_1729584894285_835533_3069">
               <lowerValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585251172_869734_3210"/>
               <upperValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585251173_451256_3211"
                           value="*"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584906002_876630_3116"
                            name="author"
                            visibility="public"
                            type="_2022x_2fe013d_1729584647379_298285_2962"
                            association="_2022x_2fe013d_1729584906001_485211_3115">
               <lowerValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585339349_230044_3275"/>
               <upperValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585339350_104972_3276"
                           value="*"/>
            </ownedAttribute>
         </packagedElement>
         <packagedElement xmi:type="uml:Class" xmi:id="_2022x_2fe013d_1729584643451_951576_2892"
                          name="Edition">
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584734501_318390_3027"
                            name="publisher"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.String"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584749342_710992_3029"
                            name="city"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.String"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584759206_169861_3031"
                            name="editionYear"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Integer"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584774710_162545_3037"
                            name="ISBN"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.String"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584894285_356613_3071"
                            name="book"
                            visibility="public"
                            type="_2022x_2fe013d_1729584640093_901664_2857"
                            association="_2022x_2fe013d_1729584894285_835533_3069"/>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584901194_630900_3093"
                            name="bookCopy"
                            visibility="public"
                            type="_2022x_2fe013d_1729584645434_826374_2927"
                            association="_2022x_2fe013d_1729584901194_966688_3092"/>
         </packagedElement>
         <packagedElement xmi:type="uml:Class" xmi:id="_2022x_2fe013d_1729584645434_826374_2927"
                          name="BookCopy">
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584786807_344758_3039"
                            name="SerialNumber"
                            visibility="public"
                            aggregation="composite">
               <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.String"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584901195_137822_3094"
                            name="edition"
                            visibility="public"
                            type="_2022x_2fe013d_1729584643451_951576_2892"
                            association="_2022x_2fe013d_1729584901194_966688_3092">
               <lowerValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585275322_418027_3231"/>
               <upperValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585275323_316078_3232"
                           value="*"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584912084_378269_3139"
                            name="owner"
                            visibility="public"
                            type="_2022x_2fe013d_1729584647379_298285_2962"
                            association="_2022x_2fe013d_1729584912084_870127_3138">
               <lowerValue xmi:type="uml:LiteralInteger" xmi:id="_2022x_2fe013d_1729585297661_406635_3252"/>
            </ownedAttribute>
         </packagedElement>
         <packagedElement xmi:type="uml:Class" xmi:id="_2022x_2fe013d_1729584647379_298285_2962"
                          name="Person">
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584906002_4311_3117"
                            name="authoredBook"
                            visibility="public"
                            type="_2022x_2fe013d_1729584640093_901664_2857"
                            association="_2022x_2fe013d_1729584906001_485211_3115">
               <lowerValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585334962_967462_3269"/>
               <upperValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585334962_271367_3270"
                           value="*"/>
            </ownedAttribute>
            <ownedAttribute xmi:type="uml:Property" xmi:id="_2022x_2fe013d_1729584912084_828896_3140"
                            name="ownedBook"
                            visibility="public"
                            type="_2022x_2fe013d_1729584645434_826374_2927"
                            association="_2022x_2fe013d_1729584912084_870127_3138">
               <lowerValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585293499_740970_3246"/>
               <upperValue xmi:type="uml:LiteralUnlimitedNatural"
                           xmi:id="_2022x_2fe013d_1729585293499_910234_3247"
                           value="*"/>
            </ownedAttribute>
         </packagedElement>
         <packagedElement xmi:type="uml:Association" xmi:id="_2022x_2fe013d_1729584894285_835533_3069"
                          name="Editionship">
            <memberEnd xmi:idref="_2022x_2fe013d_1729584894285_695564_3070"/>
            <memberEnd xmi:idref="_2022x_2fe013d_1729584894285_356613_3071"/>
         </packagedElement>
         <packagedElement xmi:type="uml:Association" xmi:id="_2022x_2fe013d_1729584901194_966688_3092"
                          name="Copies">
            <memberEnd xmi:idref="_2022x_2fe013d_1729584901194_630900_3093"/>
            <memberEnd xmi:idref="_2022x_2fe013d_1729584901195_137822_3094"/>
         </packagedElement>
         <packagedElement xmi:type="uml:Association" xmi:id="_2022x_2fe013d_1729584906001_485211_3115"
                          name="Authorship">
            <memberEnd xmi:idref="_2022x_2fe013d_1729584906002_876630_3116"/>
            <memberEnd xmi:idref="_2022x_2fe013d_1729584906002_4311_3117"/>
         </packagedElement>
         <packagedElement xmi:type="uml:Association" xmi:id="_2022x_2fe013d_1729584912084_870127_3138"
                          name="Ownership">
            <memberEnd xmi:idref="_2022x_2fe013d_1729584912084_378269_3139"/>
            <memberEnd xmi:idref="_2022x_2fe013d_1729584912084_828896_3140"/>
         </packagedElement>
      </packagedElement>
      <profileApplication xmi:type="uml:ProfileApplication"
                          xmi:id="_2022x_2fe013d_1729499324105_549946_3100">
         <appliedProfile href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML"/>
      </profileApplication>
   </uml:Model>
    ```
```

### 2.3 不带有案例的 prompt

较 2.2 去掉案例

## 三、实验结果

### 带有 example 的结果

```xml
<uml:Model xmi:type="uml:Model" xmi:id="financialSystemModel" name="FinancialSystem">
    <packagedElement xmi:type="uml:Class" xmi:id="Bank" name="Bank">
        <ownedAttribute xmi:type="uml:Property" xmi:id="branches" name="branches" visibility="public" aggregation="composite">
            <type href="#Branch"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="accounts" name="accounts" visibility="public" aggregation="composite">
            <type href="#Account"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Class" xmi:id="Branch" name="Branch">
        <ownedAttribute xmi:type="uml:Property" xmi:id="subBranches" name="subBranches" visibility="public" aggregation="composite">
            <type href="#Branch"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="customers" name="customers" visibility="public" aggregation="composite">
            <type href="#Customer"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="assetsAccount" name="assetsAccount" visibility="public">
            <type href="#Account"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Class" xmi:id="Customer" name="Customer">
        <ownedAttribute xmi:type="uml:Property" xmi:id="accounts" name="accounts" visibility="public" aggregation="composite">
            <type href="#Account"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Class" xmi:id="Account" name="Account">
        <ownedAttribute xmi:type="uml:Property" xmi:id="balance" name="balance" visibility="public">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Real"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="holder" name="holder" visibility="public">
            <type href="#Customer"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="isCredit" name="isCredit" visibility="public" aggregation="none">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Boolean"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="creditLimit" name="creditLimit" visibility="public">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Real"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Class" xmi:id="Transaction" name="Transaction">
        <ownedAttribute xmi:type="uml:Property" xmi:id="amount" name="amount" visibility="public">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Real"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="sourceAccount" name="sourceAccount" visibility="public">
            <type href="#Account"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="destinationAccount" name="destinationAccount" visibility="public">
            <type href="#Account"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Class" xmi:id="VIPCustomer" name="VIPCustomer">
        <generalization xmi:idref="Customer"/>
        <ownedAttribute xmi:type="uml:Property" xmi:id="isExemptFromFee" name="isExemptFromFee" visibility="public">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Boolean"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Class" xmi:id="Transfer" name="Transfer">
        <ownedAttribute xmi:type="uml:Property" xmi:id="transactionFee" name="transactionFee" visibility="public">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Real"/>
        </ownedAttribute>
        <ownedAttribute xmi:type="uml:Property" xmi:id="commissionRate" name="commissionRate" visibility="public">
            <type href="http://www.omg.org/spec/SysML/20181001/SysML.xmi#SysML_dataType.Real"/>
        </ownedAttribute>
    </packagedElement>

    <packagedElement xmi:type="uml:Association" xmi:id="accountHolderAssociation" name="accountHolderAssociation">
        <memberEnd xmi:idref="Customer"/>
        <memberEnd xmi:idref="Account"/>
    </packagedElement>

    <packagedElement xmi:type="uml:Association" xmi:id="accountBranchAssociation" name="accountBranchAssociation">
        <memberEnd xmi:idref="Account"/>
        <memberEnd xmi:idref="Branch"/>
    </packagedElement>
    
    <packagedElement xmi:type="uml:Association" xmi:id="transactionSourceAssociation" name="transactionSourceAssociation">
        <memberEnd xmi:idref="Transaction"/>
        <memberEnd xmi:idref="Account"/>
    </packagedElement>
    
    <packagedElement xmi:type="uml:Association" xmi:id="transactionDestinationAssociation" name="transactionDestinationAssociation">
        <memberEnd xmi:idref="Transaction"/>
        <memberEnd xmi:idref="Account"/>
    </packagedElement>
</uml:Model>
```

![null](http://123.249.71.210/yph/shiyan1.jpg)

### 不带有 example 的结果

```xml
<?xml version="1.0" encoding="UTF-8"?>
<XMI xmlns="http://www.omg.org/spec/XMI/20210701" xmlns:uml="http://www.omg.org/spec/UML/20210701">
  <uml:Model name="FinancialSystem" xmlns:sysml="http://www.omg.org/spec/SysML/20210701">
    <!-- Bank Block -->
    <uml:Class name="Bank">
      <uml:ownedAttribute name="branches" type="Branch" upperBound="*"/>
      <uml:ownedAttribute name="assetsAccount" type="Account"/>
      <uml:ownedAttribute name="customers" type="Customer" upperBound="*"/>
    </uml:Class>

    <!-- Branch Block -->
    <uml:Class name="Branch">
      <uml:ownedAttribute name="subordinateBranches" type="Branch" upperBound="*"/>
      <uml:ownedAttribute name="parentBranch" type="Branch" lowerBound="0" upperBound="1"/>
      <uml:ownedAttribute name="customers" type="Customer" upperBound="*"/>
      <uml:ownedAttribute name="accounts" type="Account" upperBound="*"/>
      <uml:ownedAttribute name="assetsAccount" type="Account"/>
    </uml:Class>

    <!-- Account Block -->
    <uml:Class name="Account">
      <uml:ownedAttribute name="balance" type="Real"/>
      <uml:ownedAttribute name="creditLimit" type="Real" lowerBound="0"/>
      <uml:ownedAttribute name="accountHolder" type="Customer"/>
      <uml:ownedAttribute name="isCreditAccount" type="Boolean"/>
    </uml:Class>

    <!-- Customer Block -->
    <uml:Class name="Customer">
      <uml:ownedAttribute name="accounts" type="Account" upperBound="*"/>
      <uml:ownedAttribute name="isVIP" type="Boolean"/>
    </uml:Class>

    <!-- VIP Account Block -->
    <uml:Class name="VIPAccount" extends="Account">
      <uml:ownedAttribute name="noAnnualFee" type="Boolean" default="true"/>
      <uml:ownedAttribute name="noTransferFee" type="Boolean" default="true"/>
    </uml:Class>

    <!-- Integrity Constraints -->
    <sysml:Constraint name="BranchLimitPerCity">
      <sysml:constraint>Number of branches per city for a bank <= 3</sysml:constraint>
    </sysml:Constraint>

    <sysml:Constraint name="CreditLimitChange">
      <sysml:constraint>Credit limit can be increased by at most 10%, or decreased, based on balance</sysml:constraint>
    </sysml:Constraint>

    <sysml:Constraint name="MaintenanceFee">
      <sysml:constraint>1% maintenance fee is deducted annually unless account is credit or branch account</sysml:constraint>
    </sysml:Constraint>

    <sysml:Constraint name="TransferFee">
      <sysml:constraint>2% commission for inter-bank transfers; 0% for intra-bank transfers</sysml:constraint>
    </sysml:Constraint>

    <sysml:Constraint name="VIPCustomer">
      <sysml:constraint>VIP status applies only to company accounts with > 1 million euros balance</sysml:constraint>
    </sysml:Constraint>

    <sysml:Constraint name="BranchAccountException">
      <sysml:constraint>Branch accounts are exempt from maintenance fees and transfer commissions</sysml:constraint>
    </sysml:Constraint>

    <!-- Associations -->
    <uml:Association name="HasBranch" memberEnd="Branch.bank, Bank.branches"/>
    <uml:Association name="HasCustomer" memberEnd="Branch.customers, Customer.accounts"/>
    <uml:Association name="OwnsAccount" memberEnd="Branch.accounts, Account.branch"/>
    <uml:Association name="HasAccountHolder" memberEnd="Account.accountHolder, Customer.accounts"/>
    <uml:Association name="TransfersMoney" memberEnd="Account.transactions, Transaction.originAccount, Transaction.destinationAccount"/>
    <uml:Association name="CreditLimitRequest" memberEnd="Customer.requestLimitChange, Branch.account"/>
  </uml:Model>
</XMI>
```

![null](http://123.249.71.210/yph/shiyan2.jpg)

## 四、实验分析

1. 大语言模型 ChatGPT 能否生成 MagicDraw 中 XMI 类型的模型？答：大模型可以生成 以 XMI 表示的 Sys 模型。
2. 上下文学习中的案例提示是否有用？答：由两次实验对比，发现案例提示是有用的，虽然案例提示的为 Books 与本问题 Banks 不相关，同时案例中的 SysML 模型也不够详细，但是添加了案例提示后，大语言模型生成的内容一方面语法格式更加接近与 MagicDraw 的真实项目（指明了聚合的方式，而不是简单的两个元素之间有关系，同时对于数据类型也有更详细的定义），另一方面，生成的模块更多，对于 Context 的体现更加准确。
3. ChatGPT 生成的效果怎么样？目前来看，ChatGPT 生成的结果是可以的，甚至超过了我们自己构建的简单的数据集，在使用过程中只需要人类来反馈修改即可。

## 五、后续工作

1. 确认了 Context+Question+Example 的 Prompt 范式，其中 Context 表示与问题相关的背景知识（可以 RAG 检索并填充）与目标 SysML 模型已经具有的上下文元素；Question 表示具体的任务，比如是由需求生成模块定义图，还是生成活动图；Example 可以由 RAG 向目前已经构建的数据集中检索并填充。
2. 探究 JSON、Plant UML、SysML v2 等格式，对于大语言模型生成结果的影响。
