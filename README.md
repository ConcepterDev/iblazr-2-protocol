## iblazr 2 protocol
Basical information about how working with iblazr 2.

iblazr sync with the app by bluetooth.

IOS: official tool for iblazr original and iblazr 2 [iblazr SDK](https://github.com/ConcepterDev/iblazr-sdk-ios)

Android: [iblazr 2 SDK](https://github.com/ConcepterDev/iblazr-sdk-android)

## Basical information
iblazr 2 works with `FAFA` service and `FAF1` characteristic

You must create and send byte array to `FAF1`

#### Array determination
For example: `{ 0x10, 0x00, 0x11, 0x7D, 0x16 }` <br>
Where: 
  1. `0x10` - command
  2. `0x00` - first "time-byte"
  3. `0x11` - second "time-byte"
  4. `0x7D` - temperature value. Available in range `0x00 - 0x7D`
  5. `0x16` - brightness value. Available in range `0x00 - 0x16`

#### Time determination
- `0x01` equal to `10ms`.
- `0x0A` equal to `100ms` and `0x64` equal to `1 second`. 

If you need send more than `2550` seconds (`0xff`), you need pass time to first "time-byte".<br>
iblazr recognize this like: 
- `{ 0x10, `**0x00**`, `**0x0A**`, 0x7D, 0x16 }` - "make flash for `100ms`"
- `{ 0x10, `**0x0A**`, `**0xFF**`, 0x7D, 0x16 }` - "make flash for `28150ms`"
- `{ 0x10, `**0x0A**`, `**0x00**`, 0x7D, 0x16 }` - "make flash for `25600ms`"
- etc...

## Available commands
        name        |           command           | time                       | temperature  | brightness
------------------- | --------------------------- | -------------------------- | ------------ | ------------
flash               |             0x10            | 0x00 - will stop light     | 0x00 - 0x7D  | 0x00 - 0x16
status              |             0x11            | 0x00 - 0xff                |    -//-      |     -//-      
constant light      |             0x16            | 0x00 - will infinite light |    -//-      |     -//-      
light specific LED  |    0x12 (0x13,0x14,0x15)    | 0x00 - 0xff                |    -//-      |     -//-      

## Feedback
Send any questions to support@concepter.co or create new issue.
