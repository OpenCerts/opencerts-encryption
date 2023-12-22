# OpenAttestation (Encryption)

To share and store documents safely, encrypt the documents with the [OpenAttestation (Encryption)](https://github.com/Open-Attestation/oa-encryption) repository. It is the codebase for the `npm` module. This module does not provide the following functionalities:

*   Programmatic wrapping of OA documents (refer to [OpenAttestation](https://www.openattestation.com/docs/developer-section/libraries/remote-files/open-attestation#wrapping-documents))

*   Programmatic verification of OA documents (refer to [OpenAttestation (Verify)](https://www.openattestation.com/docs/developer-section/libraries/remote-files/open-attestation-verify))

*   Programmatic issuance/revocation of document on the Ethereum blockchain

This library is used for encrypting OpenAttestation files when they are being transferred.

## Installation

To install OpenAttestation (Encryption) on your local machine, run the command below:

```bash
npm i @govtechsg/oa-encryption
```

***

## Usage

This section shows you how to use OpenAttestation (Encryption) to encrypt or decrypt a document.

### Encrypting a document

The following shows a code example which will encrypt a document.

>**Note:** When you run it, be sure to use different values.

```javascript
const { encryptString } = require("@govtechsg/oa-encryption");

const document = {
  version: "https://schema.openattestation.com/2.0/schema.json",
  data: {
    issuers: [
      {
        documentStore: "5924d910-8916-446a-b1c3-55e2f86dd8f3:string:0xabcdabcdabcdabcdabcdabcdabcdabcdabcdabcd",
        name: "0f737b20-9e5e-4ec4-bffd-c63002616bfd:string:University of Blockchain",
        identityProof: {
          type: "5fc379dd-cd24-4c91-a4c7-cf76f9c96d8d:string:DNS-TXT",
          location: "62e1c6c3-09a9-4e52-aaf6-9daf24d43657:string:example.com",
        },
      },
    ],
  },
  privacy: { obfuscatedData: [] },
  signature: {
    type: "SHA3MerkleProof",
    targetHash: "956e27c86d4893a971600d328e235ede886f1c00b183257a822667b69886fced",
    proof: [],
    merkleRoot: "956e27c86d4893a971600d328e235ede886f1c00b183257a822667b69886fced",
  },
};

const encryptedDocument = encryptString(JSON.stringify(document));
console.log(encryptedDocument);
```

It will display a response that looks like:

```javascript
{
  cipherText:
   'S7jca6lGDvN3ZDsPX4xc+6zLCkvRN1b1g6b0LL/IHiWn9c4JmIdmfg7fMd98fehkPMlkvScYn1/XI9ZoYA6NRjf61Kpam2A0Dx7kBR866TW+Stzbbb4AAqoXm0GX3BBvPgjhQCoGS9vJBkD0coK+DCO0Vrcdptuo2io3/zbBD6GbE5zLhnqizLrLO+RffnCeJ6LFYSUbAwBvSJv+OnNJjf+99ejaT3zKZNLB+NSu1WNG23nyzJoeYgEqg/E7i5jhD5+pZ8FvGsVQ2hM4zrnw5CvC8AfnRkR5KUEpJ4A0XJly3gQnCBN2HtIEHRmxBgPOnM2Mcm/mNVct2tqogrfyksXrLqS2YvYAEP9uGmSu3/iP2aTzS5xqiBg0UedFVQcc3cEjzaI4lXWa5t+cjzS08pssN2lT55WHsLo/XqVSTMx4/nekDl1SVm6wpfHl2htvhxvGiUF9F1tS7VpoE/+OMS7fCPkncmPKMpuUmWN79KhZS+/R0wM1sB7+HYTulYIZ3Z/vxX1YuNFSR0V6lCsVavl4tV9IhA9PvQPvmKDSyJyrD+v4AUrtEgnvyEPttfHW2MqJGGK6w9sUB3It2OvHQVXmAtVJgqpuP6cZwMlswQWfJfcjkfxWnQGCJtsCXhc7qePwxuL3C74QTFkKQcrGLGoMNcSTV5xhPxtg7zBocVs689RJkbjirhBOJajlY4NwplFga7qgyNA6yYI2BamX4fRaMq1XEuYRo8+d2kiJXSQSTEaUNQuIIsO3Nd+u8p/Dapw0xZBeyqj1Ys1N4aPFlx26OigiabXpwQNxH+ioaceU4LUsjCmF+MsPuxi3L0HLIsnvqy1LgffOswih+hqaqjHdpOMlpLcwQziD47HSOmW83jPezEEaWwiSH5eYYy4JwgsatCc+hCJEB8A8PXG1aSdRTRg+nqZQlJ4ONs+C55Svdj+6K+mdtK21qpQBIOOZjxMztubv/0/BETbPp8HDtaZdS80uLwXSNWAaf2dnbaNQkAW3idHYTgi8375FRr63/TUIeoo9Wh4YHTyjlEay/+CBokN0zREGQMaXKS/TEGxsdOIjsJjR8URyPBVFIhHNXcN1RQnxcD0WU+JvsheaoFLs/x1ITc7E',
  iv: 'TG47WMwppeS9oICk',
  tag: 'Iox0laR51y8czUw8Yx6mGQ==',
  key:
   '04d49fe8ac0a0afa5e9e2fa617551b5d7be532d0c8586a0809d7d223316d7cc5',
  type: 'OPEN-ATTESTATION-TYPE-1'
}
```

You can extract the key from the encrypted document and store the rest of the document anywhere. 


### Decrypting a document

To decrypt the document, you will need to provide the key. That makes your document content safe.

The following shows a code example which will decrypt a document that was encrypted.

>**Note:** When you run it, be sure to use different values.

```javascript
const { decryptString } = require("@govtechsg/oa-encryption");

const encryptedDocument = {
  cipherText:
    "H/smVRcwLrv7KzeMtHVYAxouaO+aaEm1jxXMw5fvHJSj3dszKK76ap17rPSa/JpiNEMXFn5pCBqnmfbveuRhjHcxKvKVSyMlbh6R+zFoge0VPwP6KDsKat/39FQddfXbbaoDz+B1vFoTc2hWFQw/IEd5DQIbj08hZiZ14A6xPfutbIiR0y5DnWQjRPWi/tPoE7aSuImWa6gr5MlJSUDcEoJ7HSqSxUS29UCn3F8WWLkaM98XYQrBDdqaKXGoG6yFyLpJkyOpdXq17qhhj5/2CNPqxZIBqIgLeVw1uUvS9XAm8QivMdtmNvTQEl1vmBALVif8FbQGuQGNnRycLo4rJpCu745qtyt9fkCblZ6aGPTt4Ghf/XtW4/dwXDJYqKotl45aY8O06/z6beWh0YOgq6qYKXdW2KscprMPtFMnoK7brKej631/NX9o7a0L83lQXQ1lL+k4JCbrQ/ZpWe3VwE8rIVd1OdVhAHDKOcAGR2n/GY1kfZ+yRjvkIuylti/bGTCl3DzBdwCi4F8ulh2uypsH1mplO+/Of1zpH/UOMLnmEOPg/ENrGZSWJSYpi/We3jVirE4rH+pXLqGLNxczS9hintWFvoV2mVFw8CqmRfakGcrEq2E5PzImBViUDZ/AUxawHtxJxKyCl9yEo/my8Mu9PFpuxQW3BryVmW1X7zCJL0DoqkoaH9hwlP2FS/cWjqiPwOSTjp+DkIuxjjnOYTcLskwEJNBpjXckvzUoz/wZ7W8gOc5cnxvY269+fEmUrsxWHcNbMu3EEFFm02EE66p9sFVQZcZqOP2Z0lINuvTh10r9fuDYDSp/u2YruZbeqJVOPHeC+5yoha8FqvmDtZ3iZcexu0X6d03Ay0xiVeIQ39+SwWs2eHspFC5FvygFJDnS4N84fuyg6E6rxpc9CUfW4YC5lyiqZfKdFHCUZ1+p8BdP0F0wMBdQmuMw1VS/CVmjW9c9P3gGAKtr5wN6XdXJY/uICdDW0RukV9JNfsdfOk0XLEqwBTbvaoRGYXoRy9Jk3KOz3xxRcWn2PwZbuf0CaZQIPJJTmU5KUBFhnFxyOZCCP6JPuHamv7ZTU5kO1b2/gZRTO9Y6RLpAFq64uFrKjzXrZWSZ",
  iv: "WK7OMSRG5ODxonBO",
  tag: "pXV7QvmTRA00OkL510pSvw==",
  key: "46b1f4f0b53e5a5b92dd8e7c9a53826a41a03d9333a501ebeb1710fcd2741420",
  type: "OPEN-ATTESTATION-TYPE-1",
};
const decryptedDocument = decryptString(encryptedDocument);
console.log(JSON.parse(decryptedDocument));
```

You will be able to retrieve your document content.

>**Important:** Remember to put back the key in the object passed to the `decryptString` function, because the key was separated from the encrypted document previously.

***

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

*   [ENCRYPTION\_PARAMETERS](#encryption_parameters)
    *   [algorithm](#algorithm)
    *   [keyLength](#keylength)
    *   [ivLength](#ivlength)
    *   [tagLength](#taglength)
    *   [version](#version)
*   [generateEncryptionKey](#generateencryptionkey)
    *   [Parameters](#parameters)
*   [encodeDocument](#encodedocument)
    *   [Parameters](#parameters-1)
*   [decodeDocument](#decodedocument)
    *   [Parameters](#parameters-2)
*   [IEncryptionResults](#iencryptionresults)
    *   [encryptString](#encryptstring)
        *   [Parameters](#parameters-3)
    *   [decryptString](#decryptstring)
        *   [Parameters](#parameters-4)

### ENCRYPTION\_PARAMETERS

To learn more about the default options from responses, see this [StackExchange post](https://crypto.stackexchange.com/questions/26783/ciphertext-and-tag-size-and-iv-transmission-with-aes-in-gcm-mode/26787).

#### algorithm

The algorithm is Galois/Counter Mode (GCM). It aims for authenticated encryption with associated data; and its specialization GMAC, for generating a
message authentication code (MAC) on data that is not encrypted.

GCM and GMAC are modes of operation for an underlying approved symmetric key block cipher. 

#### keyLength

The key size should be at least 128 bits. See this [NIST publication](http://csrc.nist.gov/publications/nistpubs/800-38D/SP-800-38D.pdf) to learn more.

#### ivLength

In Galois/Counter Mode (GCM), a 12 byte IV is strongly suggested as other IV lengths will require additional calculations. 

In principle, any IV size can be used as long as the IV doesn't repeat. However, [NIST](http://csrc.nist.gov/publications/nistpubs/800-38D/SP-800-38D.pdf) suggests only an IV size of 12 bytes needs to be supported in the implementations.

#### tagLength

Use a tag size of 64 bits at the very minimum, but it is preferable to use a tag size of the full 128 bits.

#### version

<!--Flag: Through a search in the NIST publication and the post on stackexchange, version was not found. We need to tell the users which version it is talking about.-->

### generateEncryptionKey

This request generates a random key represented as a hexadecimal string.

#### Parameters

This request supports the parameter below:

| Parameter Name  | Data Type  | Necessity | Description |
|-----------------|------------|-----------|-------------|
|`keyLengthInBits`|**[Number](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number)**| Optional  | Default `ENCRYPTION_PARAMETERS.keyLength` |


### encodeDocument

This request performs encoding on a document.

#### Parameters

This request supports the parameter below:
<!--Flag: pls check the necessity column, if it is optional or required.-->

| Parameter Name  | Data Type  | Necessity | Description |
|-----------------|------------|-----------|-------------|
|`document`|**[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**| Optional | Provide a document to encode it |

### decodeDocument

This request performs decoding on an encoded document.

#### Parameters

This request supports the parameter below:
<!--Flag: pls check the necessity column, if it is optional or required.-->

| Parameter Name  | Data Type  | Necessity | Description |
|-----------------|------------|-----------|-------------|
|`encoded`|**[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**| Optional | Provide an encoded document to decode it |

### IEncryptionResults

<!--Flag: pls clarify if we can add some description to explain IEncryptionResults -->

#### encryptString

This request encrypts a given string with symmetric AES.

##### Parameters

This request supports the parameters below:
<!--Flag: pls check the necessity column, if it is optional or required.-->

| Parameter Name  | Data Type  | Necessity | Description |
|-----------------|------------|-----------|------------|
|`document`|**[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**| Optional | Input a string to encrypt it |
| `key`  | **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** | Optional | Input an encryption key |

##### Results

`IEncryptionResults` returns cipherText cipher text in base64:

- Returns **any** `iv` in base64

- Returns **any** `tag`, which is the authenticated encryption tag in base64

- Returns **any** `key`, which is the encryption key in hexadecimal

- Returns **any** `type`, which is the encryption algorithm identifier

#### decryptString

This request decrypts a given ciphertext and its associated variables.

##### Parameters

The list below shows the relationship between parameters:

*   `$0` **[IEncryptionResults](#iencryptionresults)**

    *   `$0.cipherText` &#x20;
    *   `$0.tag` &#x20;
    *   `$0.iv` &#x20;
    *   `$0.key` &#x20;
    *   `$0.type` &#x20;

This request supports the parameters below:
<!--Flag: pls check the necessity column, if it is optional or required.-->

| Parameter Name  | Data Type  | Necessity | Description |
|-----------------|------------|-----------|------------|
|`cipherText`|**[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**| Optional | Cipher text base64 encoded |
| `tag`  | **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** | Optional | AES authentication tag base64 encoded |
| `iv` |**[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**| Optional | IV base64 encoded |
| `key`  | **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** | Optional | Decryption key hexademical encoded |
| `type` | **[String](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** | Required | Encryption algorithm identifier |

##### Results

This request returns the result in **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)**.


## Additional information

If you find a bug, have a question, or want to share an idea, reach us at our [Github repository](https://github.com/Open-Attestation/oa-encryption).
