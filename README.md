# duckyPad duckyScript Standard Library

DPDS StdLib provides **handy helper functions** to make duckyScript coding easier.

## ⚠️ Under construction!

This is part of [Jan 2026 Update Beta test](https://github.com/dekuNukem/duckyPad-Pro/blob/dsvm2/doc/beta_test.md)

## Usage

* Use latest configurator and firmware
* To include, add `USE_STDLIB` to your script. 
	* This line will be **replaced AS-IS** with the [latest StdLib source](./releases/duckypad_stdlib_latest.txt).

## Table of Contents

- [STDLIB Functions](#stdlib-functions)
    - [`WAITKEY(key_id)`](#waitkeykey_id)
    - [`MAX(a, b)`](#maxa-b)
    - [`MIN(a, b)`](#mina-b)
    - [`ABS(n)`](#absn)
    - [`MEMSET(addr, value, length)`](#memsetaddr-value-length)
    - [`MEMCPY(dest, src, n)`](#memcpydest-src-n)
- [Contribution Guidelines](#contribution-guidelines)
- [How to Contribute](#how-to-contribute)
- [Questions or Comments?](#questions-or-comments)

## STDLIB Functions

### `WAITKEY(key_id)`

Wait until a specific key is pressed

| | |
| :---: | :---: |
| **Args**  | `key_id`: Key to wait for<br>See [Key ID section](https://dekunukem.github.io/duckyPad-Pro/doc/duckyscript_info.html#key-id)|
| **Returns**  | None  |

### `MAX(a, b)`

Returns the larger of two numbers

| | |
| :---: | :---: |
| **Args**  | `a`, `b`: Numbers|
| **Returns**  | The larger value between `a` and `b` |
| **Notes** | Result affected by the current `_UNSIGNED_MATH` mode |

### `MIN(a, b)`

Returns the smaller of two numbers

| | |
| :---: | :---: |
| **Args**  | `a`, `b`: Numbers|
| **Returns**  | The smaller value between `a` and `b` |
| **Notes** | Result affected by the current `_UNSIGNED_MATH` mode |

### `ABS(n)`

Returns the absolute value of a number.

| | |
| :---: | :---: |
| **Args**  | `n`: Input number|
| **Returns**  | Absolute value of `n` |

### `MEMSET(addr, value, length)`

Fill block of memory

| | |
| :---: | :---: |
| **Args**  |`addr`: Starting address<br>`value`: Byte value (0-255) to write.<br>`length`: Number of bytes to write.|
| **Returns**  | None |
| **Notes** | For use in scratch memory region<br> |

### `MEMCPY(dest, src, n)`

Copy memory

| | |
| :---: | :---: |
| **Args**  |`dest`: Destination memory address<br>`src`: Source memory address<br>`n`: Number of bytes to copy|
| **Returns**  | None |
| **Notes** | For use in scratch memory region<br>Do not overlap|

## Contribution Guidelines

When in use, the StdLib source is added **AS-IS** to user scripts **during preprocessing**.

Therefore, please **read and follow** the guides below to ensure safety and compatibility.

#### Useful Info

* [duckyScript Reference Manual](https://github.com/dekuNukem/duckyPad-Pro/blob/dsvm2/doc/duckyscript_info.md#reserved-variables-list)
* [duckStack Virtual Machine](https://github.com/duckyPad/DuckStack)

#### Code Structure

* ONLY **function declarations** (`FUN` ... `END_FUN`) and `DEFINE` statements are allowed in StdLib source.

* Functions should be **helpful** and **not overly niche**.

* Function name should be in **ALL UPPER CASE**

* **DO NOT** use **persistent global variables** (`_GV0` - `_GV31`)

* **DO NOT** use **hard-coded memory address**

	* Let user pass addr as arg if needed

* If using **Real-Time Clock (RTC)**, always check `_RTC_IS_VALID` first and handle uninitialized RTC gracefully.

#### State Management

* If your function **modifies reserved variables** (e.g. [anything `RW` in this list](https://github.com/dekuNukem/duckyPad-Pro/blob/dsvm2/doc/duckyscript_info.md#reserved-variables-list)), you **MUST** save the original value and **restore** it before returning.

* Beware of **current math mode** affecting math results! If needed, save `_UNSIGNED_MATH` state, set new mode, perform ops, and restore before return.

* Ensure **all keys are released** before function exit.
	* E.g. no orphan `KEYDOWN`s.

* `WHILE` loops **MUST** be logically exitable
	* **DO NOT** rely on the `_ALLOW_ABORT` setting

#### Hardware Compatibility

* Use `_DP_MODEL` to check hardware version if necessary
	* Returns `1` for **original duckyPad (2020)**
		* `128x64` Screen
		* `15` Keys
	* Returns `2` for duckyPad Pro (2024).
		* `128x128` Screen
		* `20` Keys + `6` Encoder Actions
* Universal compatibility **encouraged but not required**
	* Clearly **state any incompatibility** in comments
	* **Gracefully handle incompatible hardware** if you don't want to support them

## How to Contribute

Contributions welcome!

* [Read the guidelines](#contribution-guidelines)
* Pull request
* Or post in discord
* Include a brief description in the comment, along with author credit (name, social media handle, email, etc).

## Ideas

print time?
release all keys?
memcpy?

## Questions or Comments?

Please feel free to [open an issue](https://github.com/duckyPad/DPDS-Standard-Library/issues), ask in the [official duckyPad discord](https://discord.gg/4sJCBx5), or email `dekuNukem`@`gmail`.`com`!
