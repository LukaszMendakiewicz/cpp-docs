---
description: "Learn more about: printf_s, _printf_s_l, wprintf_s, _wprintf_s_l"
title: "printf_s, _printf_s_l, wprintf_s, _wprintf_s_l"
ms.date: "3/9/2021"
api_name: ["_printf_s_l", "wprintf_s", "_wprintf_s_l", "printf_s"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["wprintf_s", "printf_s"]
helpviewer_keywords: ["wprintf_s function", "tprintf_s function", "_tprintf_s function", "printf_s_l function", "printf_s function", "_printf_s_l function", "printf function, format specification fields", "printf function, using", "_tprintf_s_l function", "wprintf_s_l function", "formatted text [C++]", "tprintf_s_l function", "_wprintf_s_l function"]
---
# `printf_s`, `_printf_s_l`, `wprintf_s`, `_wprintf_s_l`

Prints formatted output to the standard output stream. These versions of [`printf`, `_printf_l`, `wprintf`, `_wprintf_l`](printf-printf-l-wprintf-wprintf-l.md) have security enhancements, as described in [Security features in the CRT](../security-features-in-the-crt.md).

## Syntax

```C
int printf_s(
   const char *format [,
   argument]...
);
int _printf_s_l(
   const char *format,
   _locale_t locale [,
   argument]...
);
int wprintf_s(
   const wchar_t *format [,
   argument]...
);
int _wprintf_s_l(
   const wchar_t *format,
   _locale_t locale [,
   argument]...
);
```

### Parameters

*`format`*\
Format control.

*`argument`*\
Optional arguments.

*`locale`*\
The locale to use.

## Return value

Returns the number of characters printed, or a negative value if an error occurs.

## Remarks

The **`printf_s`** function formats and prints a series of characters and values to the standard output stream, **`stdout`**. If arguments follow the *`format`* string, the *`format`* string must contain specifications that determine the output format for the arguments.

The main difference between **`printf_s`** and **`printf`** is that **`printf_s`** checks the format string for valid formatting characters, whereas **`printf`** only checks if the format string is a null pointer. If either check fails, an invalid parameter handler is invoked, as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, the function returns -1 and sets **`errno`** to **`EINVAL`**.

For information on **`errno`** and error codes, see [`errno`, `_doserrno`, `_sys_errlist`, and `_sys_nerr`](../errno-doserrno-sys-errlist-and-sys-nerr.md).

**`printf_s`** and **`fprintf_s`** behave identically except that **`printf_s`** writes output to **`stdout`** rather than to a destination of type **`FILE`**. For more information, see [`fprintf_s`, `_fprintf_s_l`, `fwprintf_s`, `_fwprintf_s_l`](fprintf-s-fprintf-s-l-fwprintf-s-fwprintf-s-l.md).

**`wprintf_s`** is a wide-character version of **`printf_s`**; *`format`* is a wide-character string. **`wprintf_s`** and **`printf_s`** behave identically if the stream is opened in ANSI mode. **`printf_s`** doesn't currently support output into a UNICODE stream.

The versions of these functions with the **`_l`** suffix are identical except that they use the locale parameter passed in instead of the current thread locale.

### Generic-text routine mappings

|`TCHAR.H` routine|`_UNICODE` & `_MBCS` not defined|`_MBCS` defined|`_UNICODE` defined|
|---------------------|------------------------------------|--------------------|-----------------------|
|**`_tprintf_s`**|**`printf_s`**|**`printf_s`**|**`wprintf_s`**|
|**`_tprintf_s_l`**|**`_printf_s_l`**|**`_printf_s_l`**|**`_wprintf_s_l`**|

The *`format`* argument consists of ordinary characters, escape sequences, and (if arguments follow *`format`*) format specifications. The ordinary characters and escape sequences are copied to **`stdout`** in order of their appearance. For example, the line

```C
printf_s("Line one\n\t\tLine two\n");
```

produces the output

```Output
Line one
        Line two
```

[Format specifications](../format-specification-syntax-printf-and-wprintf-functions.md) always begin with a percent sign (**`%`**) and are read left to right. When **`printf_s`** encounters the first format specification (if any), it converts the value of the first argument after *`format`* and outputs it accordingly. The second format specification causes the second argument to be converted and output, and so on. If there are more arguments than there are format specifications, the extra arguments are ignored. The results are undefined if there are not enough arguments for all the format specifications.

> [!IMPORTANT]
> Ensure that *`format`* is not a user-defined string.
>
> Starting in Windows 10 version 2004 (build 19041), the `printf` family of functions prints exactly representable floating point numbers according to the IEEE 754 rules for rounding. In previous versions of Windows, exactly representable floating point numbers ending in '5' would always round up. IEEE 754 states that they must round to the closest even digit (also known as "Banker's Rounding"). For example, both `printf("%1.0f", 1.5)` and `printf("%1.0f", 2.5)` should round to 2. Previously, 1.5 would round to 2 and 2.5 would round to 3. This change only affects exactly representable numbers. For example, 2.35 (which, when represented in memory, is closer to 2.35000000000000008) continues to round up to 2.4. Rounding done by these functions now also respects the floating point rounding mode set by [`fesetround`](fegetround-fesetround2.md). Previously, rounding always chose `FE_TONEAREST` behavior. This change only affects programs built using Visual Studio 2019 version 16.2 and later. To use the legacy floating point rounding behavior, link with [`legacy_stdio_float_rounding.obj`](../link-options.md).

## Requirements

|Routine|Required header|
|-------------|---------------------|
|**`printf_s`**, **`_printf_s_l`**|`<stdio.h>`|
|**`wprintf_s`**, **`_wprintf_s_l`**|`<stdio.h>` or `<wchar.h>`|

The console is not supported in Universal Windows Platform (UWP) apps. The standard stream handles that are associated with the console, **`stdin`**, **`stdout`**, and **`stderr`**, must be redirected before C run-time functions can use them in UWP apps. For more compatibility information, see [Compatibility](../compatibility.md).

The console is not supported in Universal Windows Platform (UWP) apps. The standard stream handles that are associated with the console, **`stdin`**, **`stdout`**, and **`stderr`**, must be redirected before C run-time functions can use them in UWP apps. For more compatibility information, see [Compatibility](../compatibility.md).

## Example

```C
// crt_printf_s.c
/* This program uses the printf_s and wprintf_s functions
* to produce formatted output.
*/

#include <stdio.h>

int main( void )
{
   char   ch = 'h', *string = "computer";
   int    count = -9234;
   double fp = 251.7366;
   wchar_t wch = L'w', *wstring = L"Unicode";

   /* Display integers. */
   printf_s( "Integer formats:\n"
           "   Decimal: %d  Justified: %.6d  Unsigned: %u\n",
           count, count, count );

   printf_s( "Decimal %d as:\n   Hex: %Xh  C hex: 0x%x  Octal: %o\n",
            count, count, count, count );

   /* Display in different radixes. */
   printf_s( "Digits 10 equal:\n   Hex: %i  Octal: %i  Decimal: %i\n",
            0x10, 010, 10 );

   /* Display characters. */

   printf_s("Characters in field (1):\n%10c%5hc%5C%5lc\n", ch, ch, wch, wch);
   wprintf_s(L"Characters in field (2):\n%10C%5hc%5c%5lc\n", ch, ch, wch, wch);

   /* Display strings. */

   printf_s("Strings in field (1):\n%25s\n%25.4hs\n   %S%25.3ls\n",
   string, string, wstring, wstring);
   wprintf_s(L"Strings in field (2):\n%25S\n%25.4hs\n   %s%25.3ls\n",
       string, string, wstring, wstring);

   /* Display real numbers. */
   printf_s( "Real numbers:\n   %f %.2f %e %E\n", fp, fp, fp, fp );

   /* Display pointer. */
   printf_s( "\nAddress as:   %p\n", &count);

}
```

### Sample output

```Output
Integer formats:
   Decimal: -9234  Justified: -009234  Unsigned: 4294958062
Decimal -9234 as:
   Hex: FFFFDBEEh  C hex: 0xffffdbee  Octal: 37777755756
Digits 10 equal:
   Hex: 16  Octal: 8  Decimal: 10
Characters in field (1):
         h    h    w    w
Characters in field (2):
         h    h    w    w
Strings in field (1):
                 computer
                     comp
   Unicode                      Uni
Strings in field (2):
                 computer
                     comp
   Unicode                      Uni
Real numbers:
   251.736600 251.74 2.517366e+002 2.517366E+002

Address as:   0012FF78
```

## See also

[Math and floating-point support](../floating-point-support.md)\
[Stream I/O](../stream-i-o.md)\
[Locale](../locale.md)\
[`fopen`, `_wfopen`](fopen-wfopen.md)\
[`fprintf`, `_fprintf_l`, `fwprintf`, `_fwprintf_l`](fprintf-fprintf-l-fwprintf-fwprintf-l.md)\
[`scanf`, `_scanf_l`, `wscanf`, `_wscanf_l`](scanf-scanf-l-wscanf-wscanf-l.md)\
[`sprintf`, `_sprintf_l`, `swprintf`, `_swprintf_l`, `__swprintf_l`](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)\
[`vprintf` functions](../vprintf-functions.md)
