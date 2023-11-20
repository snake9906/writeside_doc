# 厂站模型维护

Start typing here...

[//]: # (```mermaid)

[//]: # (   C4Context)

[//]: # (    title System Context diagram for Internet Banking System)

[//]: # (    Enterprise_Boundary&#40;b0, "BankBoundary0"&#41; {)

[//]: # (        Person&#40;customerA, "Banking Customer A", "A customer of the bank, with personal bank accounts."&#41;)

[//]: # (        Person&#40;customerB, "Banking Customer B"&#41;)

[//]: # (        Person_Ext&#40;customerC, "Banking Customer C", "desc"&#41;)

[//]: # ()
[//]: # (        Person&#40;customerD, "Banking Customer D", "A customer of the bank, <br/> with personal bank accounts."&#41;)

[//]: # ()
[//]: # (        System&#40;SystemAA, "Internet Banking System", "Allows customers to view information about their bank accounts, and make payments."&#41;)

[//]: # ()
[//]: # (        Enterprise_Boundary&#40;b1, "BankBoundary"&#41; {)

[//]: # ()
[//]: # (            SystemDb_Ext&#40;SystemE, "Mainframe Banking System", "Stores all of the core banking information about customers, accounts, transactions, etc."&#41;)

[//]: # ()
[//]: # (            System_Boundary&#40;b2, "BankBoundary2"&#41; {)

[//]: # (                System&#40;SystemA, "Banking System A"&#41;)

[//]: # (                System&#40;SystemB, "Banking System B", "A system of the bank, with personal bank accounts. next line."&#41;)

[//]: # (            })

[//]: # ()
[//]: # (            System_Ext&#40;SystemC, "E-mail system", "The internal Microsoft Exchange e-mail system."&#41;)

[//]: # (            SystemDb&#40;SystemD, "Banking System D Database", "A system of the bank, with personal bank accounts."&#41;)

[//]: # ()
[//]: # (            Boundary&#40;b3, "BankBoundary3", "boundary"&#41; {)

[//]: # (                SystemQueue&#40;SystemF, "Banking System F Queue", "A system of the bank."&#41;)

[//]: # (                SystemQueue_Ext&#40;SystemG, "Banking System G Queue", "A system of the bank, with personal bank accounts."&#41;)

[//]: # (            })

[//]: # (        })

[//]: # (    })

[//]: # ()
[//]: # (    BiRel&#40;customerA, SystemAA, "Uses"&#41;)

[//]: # (    BiRel&#40;SystemAA, SystemE, "Uses"&#41;)

[//]: # (    Rel&#40;SystemAA, SystemC, "Sends e-mails", "SMTP"&#41;)

[//]: # (    Rel&#40;SystemC, customerA, "Sends e-mails to"&#41;)

[//]: # ()
[//]: # (    UpdateElementStyle&#40;customerA, $fontColor="red", $bgColor="grey", $borderColor="red"&#41;)

[//]: # (    UpdateRelStyle&#40;customerA, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5"&#41;)

[//]: # (    UpdateRelStyle&#40;SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10"&#41;)

[//]: # (    UpdateRelStyle&#40;SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50"&#41;)

[//]: # (    UpdateRelStyle&#40;SystemC, customerA, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20"&#41;)

[//]: # ()
[//]: # (    UpdateLayoutConfig&#40;$c4ShapeInRow="3", $c4BoundaryInRow="1"&#41;)

[//]: # (```)

[//]: # ()
[//]: # ({style="wide" sorted="desc"})

[//]: # (First Term)

[//]: # (: This is the definition of the first term.)

[//]: # ()
[//]: # (Second Term)

[//]: # (: This is the definition of the second term.)

[//]: # ()
[//]: # (<format style="bold" color="Red">Hello, world!</format>)