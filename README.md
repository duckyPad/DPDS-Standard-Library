# duckyPad duckyScript Standard Library

DPDS StdLib provides **handy helper functions** to make duckyScript coding easier.

## ⚠️ Under construction!

This is part of [Jan 2026 Update Beta test](https://github.com/dekuNukem/duckyPad-Pro/blob/dsvm2/doc/beta_test.md)

## Usage

* Use latest configurator and firmware
* To include, add `USE_STDLIB` to your script. 
	* This line will be **replaced AS-IS** with the [latest StdLib source](./releases/duckypad_stdlib_latest.txt).

## Function Docs

TBD

## Contribution Guidelines

When in use, the StdLib source is added **as-is** to user scripts during preprocessing.

Therefore, please **read and follow** the guides below to ensure safety and compatibility.

#### Useful Info

* [duckyScript Reference Manual](https://github.com/dekuNukem/duckyPad-Pro/blob/dsvm2/doc/duckyscript_info.md#reserved-variables-list)
* [duckStack Virtual Machine](https://github.com/duckyPad/DuckStack)

#### Code Structure

* ONLY **function declarations** (`FUN` ... `END_FUN`) and `DEFINE` statements are allowed in StdLib source.

* Functions should be **helpful** and **not overly niche**.

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
