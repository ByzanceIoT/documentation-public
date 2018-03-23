# Uživatelská makra

Zjištění informací o buildu binárky

```cpp
__BUILD_YEAR_LEN4__  // build year as 4-digit number, e.g 2018
__BUILD_YEAR_LEN2__  // build year as 2-digit number, e.g. 18
__BUILD_MONTH__      // build month 1 to 12
__BUILD_DAY__        // build day 1 to 31
__BUILD_HOUR__       // build hour, 24h format
__BUILD_MINUTE__     // build minute, 0 to 59
__BUILD_SECOND__     // build second, 0 to 59
```

Zjištění verze kompilátoru (ARM GCC NONEABI)

```cpp
TOSTRING(__GNUC__)
TOSTRING(__GNUC_MINOR__)
TOSTRING(__GNUC_PATCHLEVEL__));
```

Zjištění verze MBED
```cpp
MBED_MAJOR_VERSION
MBED_MINOR_VERSION
MBED_PATCH_VERSION
```

Zjištění typu targetu
```cpp
TOSTRING(__BUILD_TARGET__)
```

Build ID
```cpp
__BUILD_ID__
```

Okamžité zaseknutí programu a kritická chyba (slouží pro testování).
```cpp
__TOMAS_ZARUBA__
```

