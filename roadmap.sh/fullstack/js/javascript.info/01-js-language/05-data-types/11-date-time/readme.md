

# 📌 JavaScript Date & Time Cheat Sheet

## 🔹 Creating Dates

* `new Date()` → current date & time
* `new Date(milliseconds)` → from timestamp since `01.01.1970 UTC+0`

  * `new Date(0)` → Jan 1, 1970
  * `new Date(24*3600*1000)` → Jan 2, 1970
* `new Date(datestring)` → parses string (like `"2017-01-26"`)
* `new Date(year, month, date, hours, minutes, seconds, ms)`

  * Year: 4 digits (e.g. `2011`)
  * Month: `0 = Jan`, `11 = Dec`
  * Date defaults to `1`
  * Time parts default to `0`

<br>

## 🔹 Accessing Date Components

* `getFullYear()` → 4-digit year
* `getMonth()` → 0–11 (Jan–Dec)
* `getDate()` → day of month (1–31)
* `getDay()` → day of week (0 = Sun … 6 = Sat)
* `getHours() / getMinutes() / getSeconds() / getMilliseconds()`
* `getTime()` → timestamp (ms since 1970)
* `getTimezoneOffset()` → minutes difference from UTC
* UTC versions: `getUTCFullYear()`, `getUTCMonth()`, `getUTCHours()` …

<br>

## 🔹 Setting Date Components

* `setFullYear(year, [month], [date])`
* `setMonth(month, [date])`
* `setDate(day)`
* `setHours(hour, [min], [sec], [ms])`
* `setMinutes(min, [sec], [ms])`
* `setSeconds(sec, [ms])`
* `setMilliseconds(ms)`
* `setTime(ms)` → sets timestamp

⏩ **Auto-correct feature**:

* `new Date(2013, 0, 32)` → auto → Feb 1, 2013
* Negative/zero values roll back automatically

<br>

## 🔹 Date as Number

* `+date` or `date.getTime()` → timestamp in ms
* Subtraction works: `date2 - date1` → difference in ms

<br>

## 🔹 Measuring Time

* `Date.now()` → timestamp without creating Date object
* `performance.now()` (browser) → high precision (ms + microseconds)

<br>

## 🔹 Parsing

* `Date.parse("YYYY-MM-DDTHH:mm:ss.sssZ")` → timestamp

  * Example:

    ```js
    let ms = Date.parse("2012-01-26T13:51:50.417-07:00");
    new Date(ms);
    ```

<br>

# 📌 Tasks

### 1. Create a date

* `new Date(2012, 1, 20, 3, 12)`

### 2. Show a weekday

* `getWeekDay(date)` → "MO", "TU", … "SU"

### 3. European weekday

* `getLocalDay(date)` → Monday = 1 … Sunday = 7

### 4. Which day of month N days ago?

* `getDateAgo(date, days)`
* Uses `setDate(date.getDate() - days)` on a copy

### 5. Last day of month?

* `getLastDayOfMonth(year, month)`
* Trick: `new Date(year, month+1, 0).getDate()`

### 6. Seconds passed today

* `getSecondsToday()`

  * Now – today at 00:00

### 7. Seconds till tomorrow

* `getSecondsToTomorrow()`

  * Tomorrow 00:00 – now

### 8. Format relative date

* `formatDate(date)` rules:

  * `< 1 sec` → `"right now"`
  * `< 1 min` → `"n sec. ago"`
  * `< 1 hour` → `"m min. ago"`
  * Else → `"DD.MM.YY HH:mm"` (2-digit padded)