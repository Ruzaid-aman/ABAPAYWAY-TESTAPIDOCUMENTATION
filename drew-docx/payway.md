---
title: 'PayWay Merchant'
meta: "content.md"
---

<br>

# PayWay Merchant - Mini app

#### Browser Support

![Chrome](https://raw.githubusercontent.com/alrra/browser-logos/main/src/chrome/chrome_48x48.png) | ![Edge](https://raw.githubusercontent.com/alrra/browser-logos/main/src/edge/edge_48x48.png) |![Opera](https://raw.githubusercontent.com/alrra/browser-logos/main/src/opera/opera_48x48.png)  |
--- | --- | --- | 
Latest ✔ | Latest ✔ | Latest ✔ |

#### Installation
<br />

Using CDN:
``` javascript 
<script type="text/javascript" src="https://checkout.payway.com.kh/plugins/checkout2-0.js"></script> 
```
<br />

#### Configuration

| Key | Type| Default| Description|
| --- | --- | --- | --- |
| AbaPayway | Class |  | the class name |
| miniAppCallHandler | Function |  |<h6>The CallHandler</h6> There is a parameter (<i>handler name</i>) <br/><b></b>   |
| miniAppRegisterHandler | Function |  |<h6>The RegisterHandler</h6> There are 2 parameters: <br/><b>1.</b> handler name<br/><b>2.</b> request params as object<br/> <i>ex: {title:'My App Title'} </i>  |


<br />

#### Implementation

``` javascript 
// using the CallHandler
const callHandlerName = 'uploadFile'
const requestParams = {key:'value'}

AbaPayway.miniAppCallHandler(callHandlerName, requestParams).then((res)=>{
  console.log(res)
});

// using the RegisterHandler
const registerHandlerName = 'getFileUpload'
AbaPayway.miniAppRegisterHandler(registerHandlerName).then((res)=>{
  console.log(res)
});
```
<br />

#### CallHandler list

<table class="table-techstack-content">
<thead>
<th>No</th>
<th>Name</th>
<th>Handler name & Payload</th>
<th>Response</th>
<thead>
<!-- body -->
<tbody>
<tr>
<td>1</td>  
<td>get profile</td>  
<td>

`getProfile {}`
</td>
<td>

```json
{
    // these fields are for basic profile
    "firstName" : "John",
    "middleName": "Unknown",
    "lastName"  : "Doe",
    "fullName"  : "",
    "phone"     : "+85512345678",
    "email"     : "chanthorn.kim@hotmail.com",
    "lang"      : "en", // en, kh, zh
    "id"        : "123456", // merchant app id
    "businessId": 20342553, //Current Business
    "businessName": "DARA COFFEE",
    "outletID"  : 2343255, // Current Outlets
    "outletName": "DARA COFFEE BKK",
    "role"      : "owner", // owner, manager, cashier
    "appVersion": "4.9.12",
    "osVersion" : "14.7.1"
}
```

</td>
</tr>
<tr>
<td>2</td>
<td>
Get the default business
</td>
<td>

`getBusiness {}`


</td>
<td>
  

  ```json
{
    "paymentMethods": [
        {
            "method_name": "ABA PAY",
            "method_id": "3",
            "options": {
                "allow_disable": 0
            }
        },
        {
            "method_name": "KHQR",
            "method_id": "7",
            "options": {
                "allow_disable": 0
            }
        }
    ],
    "businessid": "7GmbC\/1OL2lBmyKB6Sh7rA==",
    "name": "FIRST 0210646",
    "currency": "USD",
    "category": "Beauty & Wellness",
    "accountNumber": "002109386",
    "outlet": {
        "address": "BTS",
        "outletid": "qYwLM\/z1i4Uw8RzczGfCNA==",
        "cashier": [],
        "name": "FIRST0210646 Titus554",
        "location": "PHNOM PENH",
        "telegramGroupID": ""
    },
    "accountHolderName": "CUSTNAME 0210646",
    "session_expired_in": "900",
    "status": {
        "code": "00",
        "tran_id": "167058119798316",
        "message": "Success!"
    }
}
  ```
  
</td>
</tr>
<tr>
<td>3</td>
<td>
Get staff list

</td>
<td>

```javascript
getStaffs {
"businessid" : 3424234234
}
```
</td>
<td>

```json
{
    [
        {
            "id": 3234234,
            "firstName": "Chanthorn",
            "lastName": "KIM",
            "phone": 23423423432
        },
    ...
    ]
} 
```
</td>
</tr>
<tr>

<td>4</td>
<td>getUserRoles</td>
<td>

`getUserRoles { }`	
</td>

<td>

```json
{
    [
        0: "Owner",
        1: "Manager",
        2: "Cashier"
    ]
}
```
</td>

</tr>
<!-- New row -->
<tr>
<td>
5
</td>
<td>Get business outlets</td>
<td>

`
getOutlets {
  "businessid": 3424234234
}
`
</td>
<td>

```json
{
    [
        {
            "name": "FOODIE by C. KIM",
            "location": "Phnom Penh",
            "address": "NA, NA, NA, Phnom Penh, Cambodia",
            "telegramGroupID": 334234508
        },
        {
            "name": "LYMALOB by C. KIM",
            "location": "Phnom Penh",
            "address": "NA, NA, NA, Phnom Penh, Cambodia",
            "telegramGroupID": 354234508
        }
    ]
    ....
}
```
</td>
</tr>

<tr>
<td>6</td>
<td>
Get all businesses and outlets
</td>
<td>

`getAllBusiness 
{} 
`

</td>
<td>

```json

{
    [
        {
            // show default business detail
            "name": "FOODIE by C. KIM",
            "category": "Foods & Beverage",
            "accountHolderName": "Chanthorn KIM",
            "accountNumber": "000094132",
            "currency": "usd",
            "paymentMethods": [
                {
                    "type": "ABA Pay",
                    "name": "ABA Pay"
                },
                {
                    "type": "KHQR",
                    "name": "KHQR"
                }
                ....
            ],
            // Default outlet
            "outlet": [
                {
                    "name": "FOODIE by C.KIM",
                    "location": "Phnom Penh",
                    "address": "NA, NA, NA, Phnom Penh, Cambodia",
                    "telegramGroupID": 334234508
                }
            ]
        },
        {
            // show default business detail
            "name": "FOODIE by C. KIM",
            "category": "Foods & Beverage",
            "accountHolderName": "Chanthorn KIM",
            "accountNumber": "000094132",
            "currency": "usd",
            "paymentMethods": [
                {
                    "type": "ABA Pay",
                    "name": "ABA Paya"
                },
                {
                    "type": "KHQR",
                    "name": "KHQR"
                }
            ....
            ],
            // Default outlet
            "outlet": [
                {
                    "name": "FOODIE by C.KIM",
                    "location": "Phnom Penh",
                    "address": "NA, NA, NA, Phnom Penh, Cambodia",
                    "telegramGroupID": 334234508
                }
            ]
        }
    ]
}

```
</td>
</tr>


<tr>
<td>7</td>
<td>Do Payment
</td>
<td>

```javascript
doPayment {
  amount: "xxx",
  account: "xxx",
  currency: "USD" // KHR,
}
```

<br>

**Account**: is a common name for unique value and it is easy to
reconcile disputes or investigate the issue.
For example, it can be orderId, ticketId, invoiceId … MUST BE
ALWAYS UNIQUE
</td>
<td>

</td>
</tr>

<tr>
<td>8</td>
<td>Get QR/Bard code scanner</td>
<td>

```javascript
doScan { }
```

</td>

<td>


</td>
</tr>

<tr>
<!-- Ne row -->
<td>9</td>
<td>Close Mini Application</td>
<td>

```javascript
closeApp { }
```

</td>
<td>

</td>
</tr>
<tr>
<td>10</td>
<td>Set Bar Title
</td>
<td>

```javascript
setBarTitle {
  title: "Home Page",
  bgColor: "#000000",
  color: "#ffffff",
  safeAreaColor: "#ffffff"
}
```

<br>

**safeAreaColor** : It uses only for iOS which allow vendor can
modify the background color for the safeAre.

</td>
<td></td>
<!-- New row -->
</tr>

<tr>
<td>11</td>
<td>Upload File
</td>
<td>

`uploadFile {}`


</td>

<td>

```json
{
  "content": "", // base64
}
```
</td>
</tr>

<tr>
<td>12</td>
<td>Get Config
</td>
<td>

`getConfig {}`

<br>

**additionalConfig** is a dynamic object based on vendor
requirements. Different vendors might get different keys/value
</td>
<td>

```json
{
    "vendorId": 100,
    "whitelist": [
        "https: //abc.com/",
        "https: //example.com/'"
    ],
    "additionalConfig": {
        "name": "Test",
        "secretKey": "",
        ...
    }
}
```
</td>
<!-- new row -->
</tr>

<tr>
<td>13</td>
<td>
Set Audio Playlist
</td>
<td>

```javascript
setPlayList {
    playId: 'id',
    playlist: [
    {
      id: '',
      url: '',
      title: '',
      thumbnail: '',
      description: '',
      bookId: '',
    }
  ]
}
```

<br>

Initial playlist and playID
- **playId**: ID of audio you want to play
- **playList**: array of playlist
- **bookId**: for redirect
</td>
<td>

```json
{
  "lat": "xxx",
  "lng": "xxx"
}
```

</td>
</tr>

<tr>
<td>14</td>
<td>Set Audio to Play
</td>
<td>

```javascript
setAudioPlay {
playId: 'id',
}
```

<br>

Set/Update playing audio
</td>
<td>

`
{}
`

</td>
</tr>

<tr>
<td>15</td>
<td>
Get current playing audio


</td>
<td>

`getPlayingId { }`

<br>

Get current playing audio on native player to sync (mark as
active) with mini app audio list

</td>
<td>

```json
{
  "data": {
    "playId": "",
    "playListId": "",
  }
}
```

</td>
</tr>

<tr>
<td>16</td>
<td>Change player mode

</td>
<td>

```javascript
switchPlayerMode {
  mode:
    'MINI', // 'MINI',
    'FULL'
}
```

<br>

Switch native player mode to small (mini) or full
</td>
<td>

</td>

</tr>


<tr>
<td>17</td>
<td>Do Account On File

</td>
<td>
Handler name:

```javascript
doAccountOnFile  
```

Params:

```javascript
{
    "qr_string": "..."
}
```

<br>

 <b>qr_string:</b>  to handle mapping account with ABA.
</td>
<td>

</td>

</tr>

</tbody>
</table>

<!-- Native app invoke -->
<br>

#### RegisterHandler list


<table>
<thead>
<td>No</td>
<td>Title</td>
<td>Handler Name</td>
<td>Response</td>
<td>Description</td>
</thead>
<tbody>
<!-- row -->
<tr>
<td>1</td>
<td>Get Status Payment	</td>
<td>

`getStatus`</td>
<td>

```json
{ 
  "transactionId": "xxx" 
}
```
</td>
<td></td>
</tr>
<!-- end row -->
<!-- row -->
<tr>
<td>2</td>
<td>Close Mini Application	</td>
<td>

`closeApp `</td>

<td>

`{}`
</td>
<td>

```javascript
this.$bridge.registerHandler("closeApp", (data, callback) => {
  callback({ status: true | false });
});
```
**Status**
- `true` close mini-app
- `false` stay on mini-app

</td>
</tr>
<!-- end row -->
<!-- row -->
<tr>
<td>3</td>
<td>Get File Upload	</td>
<td>

`getFileUpload `</td>

<td>

```json
{
  "content": "base64",
  "name": "filename.png",
  "type": "image/png"
}
```
</td>
<td>
</td>
</tr>
<!-- end row -->
<!-- row -->
<tr>
<td>4</td>
<td>Playing audio is changed</td>
<td>

`onPlayIdChange `</td>

<td>

```json
{
  "playId": "",
  "playListId": "", 
}
```
</td>
<td>
When playing audio is changed, this listener will trigger	
</td>
</tr>
<!-- end row -->
<!-- row -->
<tr>
<td>5</td>
<td>Redirect Page</td>
<td>

`redirectPage `</td>

<td>

```json
{
  "propId": "id",
  "additionalConfig": {
  "  url": "" // dynamic fields
  } // optional
}
```
</td>
<td>
Listen in root layout when the native wants to redirect to a specific page.

- `propId`: unique ID that uses to redirect page
- `additionalConfig`: optional - dynamic fields based on agreed between native and mini app 
</td>
</tr>
<!-- end row -->
<!-- row -->
<tr>
<td>6</td>
<td>On get Current Location	
</td>
<td>

`getCurrentLocation `</td>

<td>

```json
{
  "latitude": "0.000000",
  "longitude": "0.000000"
}
```
</td>
<td>
</td>
</tr>
<!-- end row -->

<tr>
<td>7</td>
<td>On get Account On File
</td>
<td>

`getAccountOnFile `</td>

<td>

```json
{
   
}
```
</td>
<td>
</td>
</tr>
<tbody>
</table>

 
<style>
  .content table {
    width: auto;
  }
  .content img {
    border: 0px;
  }
  div.page-break {
    page-break-before:always;
  }
@media print {
  @page {
    size: A4;
    margin: 1cm;
  }

  body {
    margin: 0;
    padding: 0;
  }
}
</style>





