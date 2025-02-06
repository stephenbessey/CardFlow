# DynamoDB Design Document

## Tables

### Merchant Table
**Primary Key Structure:**
- Partition Key: MerchantName (String)
- Sort Key: Token (String)

**Additional Attributes:**
- MerchantBankAccount (String)
- MerchantBank (String)

**Rationale:**
Using MerchantName/Token as the key pair enables fast merchant validation during transactions. Bank details are included to facilitate payment processing.

### TransactionLog Table
**Primary Key Structure:**
- Partition Key: MerchantName (String)
- Sort Key: Timestamp (String)

**Additional Attributes:**
- TransactionID (String)
- Amount (Number)
- Status (String)
- StatusMessage (String)
- MerchantInfo (Map)
- CardInfo (Map)

**Rationale:**
This design enables quick transaction lookups by merchant while maintaining a chronological record. Maps are used for grouped data to improve organization.

## Global Secondary Index
Created on TransactionLog table:
- Partition Key: Status (String)
- Sort Key: Timestamp (String)

**Rationale:**
Enables efficient querying of transactions by their status across all merchants.