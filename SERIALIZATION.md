`|` means choose from multiple options. Space (` `) means concatenation.

`'xy'` means a byte with leading hex digit of `x`, least significant hex digit of `y`

See `enum igbinary_type` in `igbinary.c`

```
;;;;;;;;;;;;;;;;;
; Scalars
;;;;;;;;;;;;;;;;;;

; single byte (signed or unsigned)
BYTE := '00'..'ff'
; 2 bytes (unsigned or signed)
BYTE2 := BYTE BYTE
; 4 bytes (unsigned or signed)
BYTE4 := BYTE BYTE BYTE BYTE
; 8 bytes
BYTE8 := BYTE BYTE BYTE BYTE BYTE BYTE BYTE BYTE

STRING := '11' LENGTH8 <LENGTH8 BYTE> | '12' LENGTH16 <LENGTH16 BYTE> | '13' LENGTH32 <LENGTH32 BYTE>

ARRAY_OR_REF := ARRAY|REF

ARRAY := ARRAY8|ARRAY16|ARRAY32

ARRAY8 := '14' LENGTH8 <LENGTH8 ARRAY_ENTRY>
LENGTH8 := BYTE
LENGTH16 := BYTE2
LENGTH32 := BYTE4
LENGTH64 := BYTE8

ARRAY_ENTRY := KEY ARRAY_VAL
KEY := LONG|STRING

ULONG := '06' BYTE | '08' BYTE2 | '0a' BYTE4 | '20' BYTE8
; BYTE* != '0....0' (i.e. no -0)
NEGATIVE_LONG := '07' BYTE | '09' BYTE2 | '0b' BYTE4 | '21' BYTE8
LONG := ULONG | NEGATIVE_LONG

ARRAY_VAL := ARRAY | STRING
```
