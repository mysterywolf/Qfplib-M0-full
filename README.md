# Qfplib-M0-full: 

## A free, fast and compact ARM Cortex-M0 floating-point library



## Introduction

Qfplib-M0-full is a library of IEEE 754 single- and double-precision floating-point arithmetic routines for microcontrollers based on the ARM Cortex-M0 core (ARMv6-M architecture). It should also run on Cortex-M3 and Cortex-M4 microcontrollers and will give reasonable performance, but it is not optimised for these devices.

It provides correctly rounded (to nearest, even-on-tie) addition, subtraction, multiplication, division and square root operations, and sine, cosine, tangent, arctangent, logarithm and exponential functions that give a high degree of accuracy. There are also conversion functions between floating-point values and signed or unsigned integer or fixed-point values. The library occupies less than 6 kbyte of program memory.

Qfplib-M0-full does not use any static storage. Stack use is parsimonious and statically analysable; recursion is not used.

## Licence

Qfplib-M0-full is open source, licensed under version 2 of the [GNU GPL](http://www.gnu.org/licenses/). Use at your own risk. If you wish to enquire about alternative licensing please use the e-mail address on the [home page](https://www.quinapalus.com/index.html).

## Speed

The following table compares cycle counts for Qfplib-M0-full against other libraries. Qfplib-M0-full and GCC library results are average values for non-exceptional arguments to the functions, include calling overhead, and are approximate. They were measured using an LPC11U68 microcontroller with single-cycle flash memory. Results for the Micro Digital ‘GoFast’ library—presumably optimised for speed rather than size, judging by its name—are inferred from the timings given on [this page](http://www.smxrtos.com/ussw/gofast/gofast_arm_gnu.htm) for an ARM7TDMI-based processor. The comparison here may not be not strictly fair to Qfplib-M0-full as it is not clear from their description whether Micro Digital’s library exploits features available on that processor but not on the Cortex-M0: for example, ARM mode is considerably faster and more flexible than Thumb mode, and the long multiply instructions can be used to advantage in several of the routines, especially in double precision. Micro Digital do not appear to provide public information on the code size of their library. The implementation of the basic functions does not appear to be IEEE 754 compliant with regard to rounding.

| Function     | **Qfplib-M0-full cycles** | GCC library cycles | ‘GoFast’ library cycles |
| ------------ | ------------------------- | ------------------ | ----------------------- |
| `qfp_fadd`   | **76**                    | 102                | 182                     |
| `qfp_fsub`   | **78**                    | 108                | 181                     |
| `qfp_fmul`   | **62**                    | 166                | 144                     |
| `qfp_fdiv`   | **83**                    | 475                | 799                     |
| `qfp_fcos`   | **595**                   | 3350               | 393                     |
| `qfp_fsin`   | **584**                   | 3300               | 394                     |
| `qfp_ftan`   | **671**                   | 6140               | 1090                    |
| `qfp_fatan2` | **673**                   | 4930               | 2041                    |
| `qfp_fexp`   | **261**                   | 1930               | 372                     |
| `qfp_fln`    | **277**                   | 3960               | 1321                    |
| `qfp_fsqrt`  | **67**                    | 460                | 1590                    |
| `qfp_dadd`   | **94**                    | 168                | 231                     |
| `qfp_dsub`   | **100**                   | 167                | 243                     |
| `qfp_dmul`   | **163**                   | 377                | 224                     |
| `qfp_ddiv`   | **200**                   | 1190               | 1557                    |
| `qfp_dcos`   | **1623**                  | 6162               | 951                     |
| `qfp_dsin`   | **1624**                  | 5854               | 966                     |
| `qfp_dtan`   | **1906**                  | 11371              | 2541                    |
| `qfp_datan2` | **2187**                  | 9973               | 4487                    |
| `qfp_dexp`   | **811**                   | 6655               | 1178                    |
| `qfp_dln`    | **464**                   | 4375               | 2798                    |
| `qfp_dsqrt`  | **174**                   | 1305               | 3042                    |

Note that in every case the Qfplib-M0-full **double**-precision implementation is faster than the corresponding GCC **single**-precision implementation, sometimes by a very large factor.

The ARM CMSIS implementations of the scientific functions, despite their name ‘FastMath’, appear to be many times slower than Qfplib-M0-full. For example, the average execution time for ARM's single-precision cosine function (compiled using GCC) is about 3880 cycles, virtually independent of the optimisation flags used.

## Limitations and deviations from the IEEE 754 standard

On input and output NaNs are converted to infinities and denormals are flushed to zero.

## Function ranges and accuracy

Subject to the limitations and deviations mentioned above, the addition, subtraction, multiplication, division and square root functions all produce correctly rounded (to nearest, even-on-tie) results. This has been verified using many billions of test cases, both random and contrived.

Other functions generally give results accurate to approximately 1 ulp (‘unit in last place’). Accuracy is poorer where a tiny change in an argument results in a change in the result of a large number of ulps, such as when taking the logarithm of a value near 1 or the sine of a value near a multiple of π. Accurate handling of such cases consumes a large amount of code space and is seldom if ever needed.

The single-precision trigonometric functions require an argument between –128 and +128; the double-precision trigonometric functions require an argument between –1024 and +1024.

The comparison functions return zero if its arguments are equal (negative zero is equal to positive zero) or plus or minus one if its first argument is respectively greater than or less than its second.

## Conversion functions

A comprehensive range of functions is provided to convert between floating-point data and signed and unsigned fixed-point and integer data. They are as follows.

- `qfp_float2int`
- `qfp_float2fix`
- `qfp_float2uint`
- `qfp_float2ufix`
- `qfp_int2float`
- `qfp_fix2float`
- `qfp_uint2float`
- `qfp_ufix2float`
- `qfp_int642float`
- `qfp_fix642float`
- `qfp_uint642float`
- `qfp_ufix642float`
- `qfp_float2int64`
- `qfp_float2fix64`
- `qfp_float2uint64`
- `qfp_float2ufix64`
- `qfp_double2int`
- `qfp_double2fix`
- `qfp_double2uint`
- `qfp_double2ufix`
- `qfp_double2int64`
- `qfp_double2fix64`
- `qfp_double2uint64`
- `qfp_double2ufix64`
- `qfp_int2double`
- `qfp_fix2double`
- `qfp_uint2double`
- `qfp_ufix2double`
- `qfp_int642double`
- `qfp_fix642double`
- `qfp_uint642double`
- `qfp_ufix642double`
- `qfp_double2float`
- `qfp_float2double`

## Other functions

You may also be interested in the `qfp_float2str` and `qfp_str2float` functions provided as part of [Qfplib-M0-tiny](https://github.com/mysterywolf/Qfplib-M0-tiny) library.

Visit http://www.quinapalus.com/qfplib.html for more information.