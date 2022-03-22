

> The flat file schema defines the structure of a flat file, and this enables Mule to write and read in this format.
```ffd
form: FLATFILE
structures:
- id: 'BatchReq'
  name: Batch Request
  data:
  - { idRef: 'RQH' }
  - groupId: 'Batch'
    count: '>1'
    items:
    - { idRef: 'BCH' }
    - { idRef: 'TDR', count: '>1' }
    - { idRef: 'BCF' }
  - { idRef: 'RQF' }
segments:
- id: 'RQH'
  name: "Request File Header Record"
  values:
  - { name: 'Record Type', type: String, length: 3, tagValue: 'RQH' }
  - { name: 'File Creation Date', type: Date, length: 8 }
  - { name: 'File Creation Time', type: Time, length: 4 }
  - { name: 'Unique File Identifier', type: String, length: 10 }
  - { name: 'Currency', type: String, length: 3 }
- id: 'BCH'
  name: "Batch Header Record"
  values:
  - { name: 'Record Type', type: String, length: 3, tagValue: 'BAT' }
  - { name: 'Sequence Number', type: Integer, format: { justify: zeroes }, length: 6 }
  - { name: 'Batch Function', type: String, length: 1, tagValue: 'H' }
  - { name: 'Company Name', type: String, length: 30 }
  - { name: 'Unique Batch Identifier', type: String, length: 10 }
- id: 'TDR'
  name: "Transaction Detail Record"
  values:
  - { name: 'Record Type', type: String, length: 3, tagValue: 'BAT' }
  - { name: 'Sequence Number', type: Integer, format: { justify: zeroes }, length: 6 }
  - { name: 'Batch Function', type: String, length: 1, tagValue: 'D' }
  - { name: 'Account Number', type: String, length: 10 }
  - { name: 'Amount', type: Integer, format: { justify: zeroes }, length: 10 }
  - { name: 'Type', type: String, length: 2 }
- id: 'BCF'
  name: "Batch Footer Record"
  values:
  - { name: 'Record Type', type: String, length: 3, tagValue: 'BAT' }
  - { name: 'Sequence Number', type: Integer, format: { justify: zeroes }, length: 6 }
  - { name: 'Batch Function', type: String, length: 1, tagValue: 'T' }
  - { name: 'Batch Transaction Amount', type: Integer, format: { justify: zeroes }, length: 10 }
  - { name: 'Type', type: String, length: 2 }
  - { name: 'Batch Transaction Count', type: Integer, format: { justify: zeroes }, length: 6 }
  - { name: 'Unique Batch Identifier', type: String, length: 10 }
- id: 'RQF'
  name: "Request File Footer Record"
  values:
  - { name: 'Record Type', type: String, length: 3, tagValue: 'RQF' }
  - { name: 'File Batch Count', type: Integer, format: { justify: zeroes }, length: 4 }
  - { name: 'File Transaction Count', type: Integer, format: { justify: zeroes }, length: 6 }
  - { name: 'File Transaction Amount', type: Integer, format: { justify: zeroes }, length: 12 }
  - { name: 'Type', type: String, length: 2 }
  - { name: 'Unique File Identifier', type: String, length: 10 }
```
> One of the most common flat file examples is a comma-separated values (CSV) file. In a CSV file, table data is represented by lines of ASCII text. The value of each table cell in the example below is separated by a comma and each row is represented by a new line.

> Keeping data in flat files provides a reliable and trustworthy method for transferring data remotely, while ensuring data retains its original state and authenticity. Since flat files do not require extensive storage space, they are often used in data warehouse and data lake projects to store large volumes of unstructured and semi-structured data.
