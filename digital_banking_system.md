# analyst_portfolio

# Digital banking system - SEPA payments
ISO 20022, the International Organisation for Standardisation, have used XML as the international standard format for their payment messages.

- [SEPA Credti Transfer rule book](https://www.europeanpaymentscouncil.eu/sites/default/files/kb/file/2018-03/EPC005-18%20SCT%20Rulebook%202018%20Change%20Request%20Public%20Consultation%20Document.pdf)

- [SEPA CREDIT TRANSFER SCHEME
INTERBANK
IMPLEMENTATION GUIDELINES](https://www.europeanpaymentscouncil.eu/sites/default/files/kb/file/2018-11/EPC115-06%20SCT%20Interbank%20IG%202019%20V1.0.pdf)

# Terminology of files that are used for communication between originator and beneficiary

|Term|Description|
|--|---|
|PACS.008|payment(s) send from originator to beneficiary bank in XML file.|
|PACS.002|Status report - can be positive or negative (RJCT or ACCP) in XML file. Sends beneficiary bank to originator in XML file. This status report is in pre-settlement phase.|
|PACS.004|Form of a return the payment (return based on un-processable PACS.008 payment). Sends beneficiary bank to originator in XML file. Also use for accpetation of recalls.|
|CAMT.056| Recall in XML file.|
|CAMT.029|Negative answers to incoming recalls|
|CAMT.027|Claim non-receipt. SCT Inquiry. This message is sent by originator (originator bank), in case that beneficiary has not received a payment.|
|CAMT.087|Claim for value date correction.|

# High-level visualization of payment messages

Origbank - bank of the originator, Benbank - bank of the beneficiary

1. Originator sends payment in pacs.008 XML file
2. If XML file is correct/structured as should be/have all mandatory elements then is accepted by the beneficiary bank
3. Beneficiary bank can accept this payment and send status report (response) as pacs.002 with ACCEPTED code
4. Beneficiary bank can not accept this payment and send a status report (response) as pacs.002 with REJECTED code
![Sequence diagram - high-level communication](http://www.plantuml.com/plantuml/png/ZP5DIyD048Rl-ojUyD8AbMWLfGUfBTPB4Qa7pzlDDAxTxCJTYQL8_xlDOlfH49oGmywyppE76KRHGUhIASDU0ZjmiCLS--MkCIUVtge8N5UOaT7EWHVWMWgsla2broLvKS2EHgzttv83HF9vc-h4BZgLDl4Yo-ww2aYn5cdv0SxnAbhgY40L1m7xrh33hnAkdU25enNxHKtOhQ60FxsjPAKZj35K2UNepEY3Z52UZEGYuPaAlLUg_mazorwQAlbyhff_Mt5fVQM3BX7fioPl2DyAU0Y1LsDs771sdJMV0gPsGLFhQSGXft0wVMgkCT9csPp5vx_ZyNWoURnHcyDDxI6RHKUkBEltBnTDzrIJPSRSQk1Ov5dem69ITkIsy94ZzV7sReKKDcf8FgzBzmC0)
```plantuml
@startuml
control origbank
control benbank

group Recall of outgoing payment
   origbank --> benbank: send payment(s) (pacs.008)
   benbank --> origbank: * Status report on payment (pacs.002)
   alt Positive reply 
     benbank --> origbank: payment was accepted (Rejected)
   else Negative reply
    benbank --> origbank: payment was not accepted      
   end
end



skinparam sequence {
  ArrowColor #404040
  LifeLineBorderColor #404040
  GroupBackgroundColor #CCFFE5
}

skinparam control {
  BorderColor #00331f
  BackgroundColor #00cc7a  
}

skinparam note {
  Bordercolor Black
  Backgroundcolor White
 }
@enduml
```

# Recall process in digitan banking system SEPA only (between two banks (bank1 and bank2)

![Recall process](http://www.plantuml.com/plantuml/png/RP713jem38RlUGfBky0aK2cmQHmcHZLsGTC4atREKjD5f7QNE4neujr7Ma1qggCSuj__vrXU1z5UOksKOHBF3dvgEirwhrofodDiO8z6EmTy18vIiQKA6dsfaKG1T4QOJ3vsfXKSaCh1WhjUQ3Bej5WcyFWxOX0O6LtBD5k-6pyS-HCvMy5RE8YM6C1Zmrw02SmGfT4cJBCiRodQ2NpZOCMUCHdT9MK7w7kKw6aKncd4Zeib5D_34xXeWUW2mbUiT8yu20piOlfQ8bewOn2RR4oFIVCFVZw6DbeqbIhTMuIJfKPxNKD8Ov51-Ai0FddFVmfsxE7D8aj70Upi4NUMSCE-HF-_-YLjRwFDAQsHohjS5DljvwMwldPwh3qrwh6oR3wV7LEsZqcACUyrG1z4BFX2CMtjnjtCFKQN__7B2YgugZLI6Mlt3m00)

```plantuml
@startuml
control bank2
control bank1

group Recall of outgoing payment
   bank1 -->bank2: Cancelation request (camt.056)
   bank2 --> bank1: * Status report on cancelation request (pacs.002)
   alt Positive reply
     bank2 --> bank1: Return(s) of canceled CTs (pacs.004)
   else Negative reply
    bank2 --> bank1: Resolution of investigation (camt.029r3)      
   end
end



skinparam sequence {
  ArrowColor #404040
  LifeLineBorderColor #404040
  GroupBackgroundColor #CCFFE5
}

skinparam control {
  BorderColor #00331f
  BackgroundColor #00cc7a  
}

skinparam note {
  Bordercolor Black
  Backgroundcolor White
 }
@enduml
```
