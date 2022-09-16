![Build](https://img.shields.io/github/workflow/status/georgesmith46/bcbp/Release?style=for-the-badge)
![License](https://img.shields.io/github/license/georgesmith46/bcbp?style=for-the-badge)
![Bundlephobia](https://img.shields.io/bundlephobia/minzip/bcbp?style=for-the-badge)
![Version](https://img.shields.io/npm/v/bcbp?style=for-the-badge)

# BCBP

Encoding/decoding library for the IATA Bar Coded Boarding Pass

- Supports version 6 of the BCBP standard
- Supports any number of legs

## Getting started

### Installation

Installation is done using the
[`npm install` command](https://docs.npmjs.com/getting-started/installing-npm-packages-locally):

```bash
$ npm install bcbp
```

## Encode

```ts
encode(data: BoardingPassData) => string
```

### Example

```js
import { encode } from "bcbp";

let output = encode({
  legs: [
    {
      operatingCarrierPNR: "ABC123",
      departureAirport: "YUL",
      arrivalAirport: "FRA",
      operatingCarrierDesignator: "AC",
      flightNumber: "0834",
      flightDate: new Date("2020-08-13T00:00:00.000Z"),
      compartmentCode: "F",
      seatNumber: "001A",
      checkInSequenceNumber: "0025",
      passengerStatus: "1",
    },
  ],
  passengerName: "DESMARAIS/LUC",
});

console.log(output);
// M1DESMARAIS/LUC       EABC123 YULFRAAC 0834 226F001A0025 100
```

## Decode

```ts
decode(bcbp: string, referenceYear?: number ) => BoardingPassData
```

### Example

```js
import { decode } from "bcbp";

let output = decode(
  "M1DESMARAIS/LUC       EABC123 YULFRAAC 0834 226F001A0025 100"
);

console.log(output.passengerName);
// DESMARAIS/LUC
```

### Reference Year

Define the year which is used when parsing date fields. If this is undefined, the current year is used.

```js
import { decode } from "bcbp";

let output = decode(
  "M1DESMARAIS/LUC       EABC123 YULFRAAC 0834 226F001A0025 100",
  2010
);

console.log(output.legs[0].flightDate.toISOString());
// "2010-08-14T00:00:00.000Z"
```

# BoardingPassData

An object which is to be passed as input to the `encode` method and is the return value of the `decode` method.

```js
const bcbpObject = {
  // Passenger Name (string)
  passengerName: "DESMARAIS/LUC",

  // Passenger Description (string)
  passengerDescription: "1",

  // Source of check-in (string)
  checkInSource: "W",

  // Source of Boarding Pass Issuance (string)
  boardingPassIssuanceSource: "W",

  // Date of Issue of Boarding Pass (Date)
  issuanceDate: new Date("2016-08-12T00:00:00.000Z"),

  // Document Type (string)
  documentType: "B",

  // Airline Designator of boarding pass issuer (string)
  boardingPassIssuerDesignator: "AC",

  // Baggage Tag Licence Plate Number(s) (string)
  baggageTagNumber: "0014123456003",

  // 1st Non-Consecutive Baggage Tag Licence Plate Number (string)
  firstBaggageTagNumber: "0014123456003",

  // 2nd Non-Consecutive Baggage Tag Licence Plate Number (string)
  secondBaggageTagNumber: "0014123456003",

  // Type of Security Data (string)
  securityDataType: "1",

  // Security Data (string)
  securityData:
    "GIWVC5EH7JNT684FVNJ91W2QA4DVN5J8K4F0L0GEQ3DF5TGBN8709HKT5D3DW3GBHFCVHMY7J5T6HFR41W2QA4DVN5J8K4F0L0GE",

  // Repeatable legs data (array)
  legs: [
    {
      // Operating carrier PNR Code (string)
      operatingCarrierPNR: "ABC123",

      // From City Airport Code (string)
      departureAirport: "YUL",

      // To City Airport Code (string)
      arrivalAirport: "FRA",

      // Operating carrier Designator (string)
      operatingCarrierDesignator: "AC",

      // Flight Number (string)
      flightNumber: "0834",

      // Date of Flight (Date)
      flightDate: new Date("2016-08-13T00:00:00.000Z"),

      // Compartment Code (string)
      compartmentCode: "F",

      // Seat Number (string)
      seatNumber: "001A",

      // Check-in Sequence Number (string)
      checkInSequenceNumber: "0025",

      // Passenger Status (string)
      passengerStatus: "1",

      // Airline Numeric Code (string)
      airlineNumericCode: "014",

      // Document Form/Serial Number (string)
      serialNumber: "1234567890",

      // Selectee indicator (string)
      selecteeIndicator: "0",

      // International Documentation Verification (string)
      internationalDocumentationVerification: "1",

      // Marketing carrier designator (string)
      marketingCarrierDesignator: "AC",

      // Frequent Flyer Airline Designator (string)
      frequentFlyerAirlineDesignator: "AC",

      // Frequent Flyer Number (string)
      frequentFlyerNumber: "1234567890123",

      // ID/AD Indicator (string)
      idIndicator: "0",

      // Free Baggage Allowance (string)
      freeBaggageAllowance: "20K",

      // Fast Track (boolean)
      fastTrack: true,

      // For individual airline use (string)
      airlineInfo: "LX58Z",
    },
  ],
};
```


## License

MIT
