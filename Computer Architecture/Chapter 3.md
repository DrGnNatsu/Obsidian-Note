___
# Integer Operations
## Integer Additions
![[IntegerAddition.png]]
- Overflow: result out of range 
	- Adding +ve and –ve operands, no overflow 
	- Adding two +ve operands 
		- Overflow if the result sign is 1 
	- Adding two –ve operands 
		- Overflow if the result sign is 0
## Integer subtraction
- Add negation (2’s complement) of the second operand.
## Deal with Overflow
- Some languages (e.g., C) ignore overflow: Use MIPS `addu, addui, subu` instructions (the `u` means unsigned = will not check the signed bit of the result, meaning that they do not care about the overflow)
- Other languages (e.g., Ada and Fortran) require an exception to be raised. 
	- Use MIPS `add, addi, and sub` instructions. 
	- On overflow, invoke the exception handler (hardware) 
		- Save PC in the exception program counter (EPC) register. 
		- Jump to predefined handler address. 
		- The `mfc0` (move from coprocessor reg) instruction can retrieve the EPC value, which can be returned after corrective action.
## Hardware for Multiplications

The length of the product is the sum of the operand lengths (`4 bits` * `4 bits` = resulting length `8 bits`).
## Hardware Operations
## MIPS Multiplication Instructions
- Two 32-bit registers for product 
	- HI: most-significant 32 bits 
	- LO: least-significant 32 bits 
- Instructions:
	- `mult rs, rt / multu rs, rt` 
		- 64-bit product in `HI/LO` 
	- `mfhi rd / mflo rd: mfhi = move from high, mflo = move from low 
	- Move from `HI/LO` to `rd`. 
		- Can test the HI value to see if the product overflows 32 bits 
	- `mul rd, rs, rt` 
		- ONLY the least-significant 32 bits of product → `rd`
## Division
![[Division.png]]
- N-bit operands yield n-bit quotient and remainder
- Long division approach:
	- If divisor ≤ dividend bits: 1 bit in quotient, subtract 
	- Otherwise: 0 bit in quotient, bring down the next dividend bit.
- Restoring divisor:
	- Do the subtraction, and if the remainder goes < 0, add the divisor back. 
	- Signed division:
		- Divide using absolute values. 
		- Adjust the sign of the quotient and remainder as required
## Hardware for Division
## Optimised Hardware
## MIPS division instructions
- Use HI/LO registers for the result. 
	- HI: 32-bit remainder 
	- LO: 32-bit quotient 
- Instructions 
	- `div rs, rt / divu rs, rt` : `rs` is divider, `rt` is divisor.
	- No overflow or divide-by-0 checking: What are the values in HI/LO if the divisor is 0? **DO NOT CHECK DIVIDE BY 0** → Must write the branch to check divisor is 0 or not
- Software must perform checks if required: Use `mfhi, mflo` to access the result.
# Floating Points Numbers
## Floating Points
- Representation for non-integral numbers: Including very small and very large numbers 
- Like scientific notation 
	- Normalised: $−2.54 × 10^5$
	- Not normalised: $987.3 * 10^-3$
- In binary: $±1.xxxx_2 × 2^y$, The `y` components can be written in decimal to be readable.
- In ANSI C: float or double
## Floating Point Standard
- Defined by IEEE Std 754-1985 (IEEE-754):
	- Developed in response to divergence of representations 
	- Portability issues for scientific code 
- Now almost universally adopted 
- Two representations:
	- Single precision (32-bit): float (C) 
	- Double precision (64-bit): double (C)
## IEEE-754 format
![[IEEE-754_format.png]]
- S: sign bit (0 non-negative, 1 negative) 
- Normalize significand: 1.0 ≤ |significand| < 2.0 
	- Always has a leading pre-binary-point 1 bit, so no need to represent it explicitly (hidden bit) 
	- Significand is a Fraction with the `1.` restored: $0 ≤ |Fraction| < 1.0$
- **Exponent = actual exponent + Bias**: bias used to make sure the number is positive
	- Ensures the exponent is unsigned 
	- Single: Bias = 127; Double: Bias = 1023 
## Single Precision Range
- Exponents 00000000 and 11111111 are reserved 
- Smallest value 
	- Exponent: 00000001 actual exponent = 1 – 127 = –126 
	- Fraction: 000…00 significand = 1.0 
	- $±1.0 × 2^{-126} ≈ ± 1.2 × 10^{-38}$
- Largest value 
- exponent: 11111110 actual exponent = 254 – 127 = +127 
- Fraction: 111…11 significand ≈ 2.0 
- $±2.0 × 2^{127} ≈ ± 3.4 × 10^{38}$
## Double Precision Range
- Exponents 0000...00 and 111...111 are reserved 
- Smallest value 
	- Exponent:  00000000001 actual exponent = 1 – 1023 = –1022
	- Fraction: 000…00 significand = 1.0 
	- $±1.0 × 2^{−1022} ≈ ± 2.2 × 10^{-38}$
- Largest value 
- exponent: 11111110 actual exponent = 254 – 127 = +127 
- Fraction: 111…11 significand ≈ 2.0 
- $±1.0 × 2^{1022} ≈ ± 2.2 × 10^{-38}$
### Load Floating Point
load 7.5 to register

```asm
lui $t0, 0x40F0
ori $t0, $t0, 0x0 # $t0 = 0x40F00000
addi $sp, $sp, -4
sw $t0, 0($sp)
luc1 $f3, 0($sp)
addi $sp, $sp, 4
```





