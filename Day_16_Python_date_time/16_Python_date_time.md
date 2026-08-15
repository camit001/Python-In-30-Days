<div align="center">
  <h1>Python In 30 Days: Day 16 - Python Date Time</h1>

  <sub>Author:
  <a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
  </sub>
</div>

[<< Day 15](../Day_15_Python_type_errors/15_Python_type_errors.md) | [Day 17 >>](../Day_17_Exception_handling/17_Exception_handling.md)

**Python In 30 Days**

- [📘 Day 16](#-day-16)
  - [Python `datetime`](#python-datetime)
    - [Getting `datetime` Information](#getting-datetime-information)
    - [Formatting Date Output Using `strftime`](#formatting-date-output-using-strftime)
    - [String to Time Using `strptime`](#string-to-time-using-strptime)
    - [Using `date` from `datetime`](#using-date-from-datetime)
    - [Time Objects to Represent Time](#time-objects-to-represent-time)
    - [Difference Between Two Points in Time](#difference-between-two-points-in-time)
    - [Difference Between Two Points in Time Using `timedelta`](#difference-between-two-points-in-time-using-timedelta)
    - [Working with Time Zones](#working-with-time-zones)
    - [Adding and Subtracting Dates](#adding-and-subtracting-dates)
    - [Comparing Dates](#comparing-dates)
  - [💻 Exercises: Day 16](#-exercises-day-16)

# 📘 Day 16

## Python `datetime`

Python provides the `datetime` module to work with dates and times.

The main classes we will use are:

- `date` - represents a calendar date
- `datetime` - represents both date and time
- `time` - represents a time of day
- `timedelta` - represents a duration or difference between dates and times
- `timezone` - represents a fixed UTC offset

You can inspect the contents of a module with `dir()`:

```py
import datetime

print(dir(datetime))
```

The output contains many names, including `date`, `datetime`, `time`, `timedelta`, `timezone`, and `tzinfo`.

For this lesson, we will focus on the most useful date and time operations.

> **Date used in the examples:** 15 August 2026. This lesson uses current, recent dates instead of the old 2019-2022 examples found in many older Python tutorials.

---

## Getting `datetime` Information

We can use `datetime.now()` to get the current local date and time.

```py
from datetime import datetime

now = datetime.now()

print(now)
print("Day:", now.day)
print("Month:", now.month)
print("Year:", now.year)
print("Hour:", now.hour)
print("Minute:", now.minute)
print("Second:", now.second)

timestamp = now.timestamp()
print("Timestamp:", timestamp)
```

The exact output depends on when the program runs.

For example, on 15 August 2026, the date portion will be:

```text
2026-08-15
```

### Unix Timestamp

A Unix timestamp represents the number of seconds elapsed since:

```text
1 January 1970 00:00:00 UTC
```

You can get a timestamp from a `datetime` object:

```py
from datetime import datetime

now = datetime.now()

print(now.timestamp())
```

You can also convert a timestamp back to a `datetime`:

```py
from datetime import datetime

timestamp = 1786752000

date_time = datetime.fromtimestamp(timestamp)

print(date_time)
```

---

## Formatting Date Output Using `strftime`

`strftime()` converts a date or datetime object into a formatted string.

```py
from datetime import datetime

now = datetime.now()

print(now.strftime("%H:%M:%S"))
print(now.strftime("%m/%d/%Y, %H:%M:%S"))
print(now.strftime("%d/%m/%Y, %H:%M:%S"))
```

Example formats:

```text
time: 18:21:40
time one: 08/15/2026, 18:21:40
time two: 15/08/2026, 18:21:40
```

The exact time will depend on when the program is executed.

### Common `strftime` Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `%Y` | Four-digit year | `2026` |
| `%y` | Two-digit year | `26` |
| `%m` | Month as a number | `08` |
| `%B` | Full month name | `August` |
| `%b` | Short month name | `Aug` |
| `%d` | Day of month | `15` |
| `%A` | Full weekday name | `Saturday` |
| `%a` | Short weekday name | `Sat` |
| `%H` | Hour, 24-hour format | `18` |
| `%I` | Hour, 12-hour format | `06` |
| `%M` | Minute | `21` |
| `%S` | Second | `40` |
| `%p` | AM/PM | `PM` |

Example:

```py
from datetime import datetime

now = datetime.now()

formatted = now.strftime("%A, %d %B %Y")
print(formatted)
```

Possible output on the current lesson date:

```text
Saturday, 15 August 2026
```

---

## String to Time Using `strptime`

`strptime()` converts a string into a `datetime` object.

This is useful when dates arrive as strings from files, APIs, databases, or user input.

```py
from datetime import datetime

date_string = "15 August, 2026"

date_object = datetime.strptime(
    date_string,
    "%d %B, %Y"
)

print("date_string =", date_string)
print("date_object =", date_object)
```

Output:

```text
date_string = 15 August, 2026
date_object = 2026-08-15 00:00:00
```

The format must match the input string.

For example:

```py
from datetime import datetime

date_string = "15/08/2026"

date_object = datetime.strptime(
    date_string,
    "%d/%m/%Y"
)

print(date_object)
```

### `strptime()` vs `strftime()`

Remember:

```text
strptime = string → datetime
strftime = datetime → string
```

A simple memory trick:

```text
p = parse
f = format
```

---

## Using `date` from `datetime`

The `date` class represents a calendar date without a time.

```py
from datetime import date

d = date(2026, 8, 15)

print(d)
print("Year:", d.year)
print("Month:", d.month)
print("Day:", d.day)
```

Get today's date:

```py
today = date.today()

print("Current date:", today)
print("Current year:", today.year)
print("Current month:", today.month)
print("Current day:", today.day)
```

On the lesson's current date, the result is:

```text
Current date: 2026-08-15
Current year: 2026
Current month: 8
Current day: 15
```

---

## Time Objects to Represent Time

The `time` class represents a time of day without a date.

```py
from datetime import time

# time(hour=0, minute=0, second=0)
a = time()

print("a =", a)
```

Output:

```text
a = 00:00:00
```

Create a specific time:

```py
b = time(10, 30, 50)

print("b =", b)
```

Output:

```text
b = 10:30:50
```

Keyword arguments can also be used:

```py
c = time(
    hour=10,
    minute=30,
    second=50
)

print("c =", c)
```

Microseconds are supported:

```py
d = time(
    hour=10,
    minute=30,
    second=50,
    microsecond=200555
)

print("d =", d)
```

Output:

```text
d = 10:30:50.200555
```

---

## Difference Between Two Points in Time

We can subtract two `date` objects to find the difference between them.

```py
from datetime import date

today = date(2026, 8, 15)
future_date = date(2027, 1, 1)

time_left = future_date - today

print("Time left:", time_left)
```

Output:

```text
Time left: 139 days, 0:00:00
```

We can also subtract two `datetime` objects.

```py
from datetime import datetime

t1 = datetime(
    year=2026,
    month=8,
    day=15,
    hour=10,
    minute=0
)

t2 = datetime(
    year=2026,
    month=8,
    day=20,
    hour=12,
    minute=30
)

diff = t2 - t1

print("Difference:", diff)
```

Output:

```text
Difference: 5 days, 2:30:00
```

---

## Difference Between Two Points in Time Using `timedelta`

`timedelta` represents a duration.

```py
from datetime import timedelta

t1 = timedelta(
    weeks=12,
    days=10,
    hours=4,
    seconds=20
)

t2 = timedelta(
    days=7,
    hours=5,
    minutes=3,
    seconds=30
)

t3 = t1 - t2

print("t3 =", t3)
```

Output:

```text
t3 = 86 days, 22:56:50
```

### Creating a Future Date

`timedelta` can also be added to a date.

```py
from datetime import date, timedelta

today = date(2026, 8, 15)

future_date = today + timedelta(days=30)

print("Today:", today)
print("After 30 days:", future_date)
```

Output:

```text
Today: 2026-08-15
After 30 days: 2026-09-14
```

### Creating a Previous Date

```py
from datetime import date, timedelta

today = date(2026, 8, 15)

previous_date = today - timedelta(days=30)

print("Today:", today)
print("30 days earlier:", previous_date)
```

Output:

```text
Today: 2026-08-15
30 days earlier: 2026-07-16
```

---

## Working with Time Zones

Date and time handling becomes more important when applications work across different countries.

Python provides timezone-aware datetime objects.

```py
from datetime import datetime, timezone

utc_now = datetime.now(timezone.utc)

print("UTC time:", utc_now)
```

For fixed offsets:

```py
from datetime import datetime, timezone, timedelta

india_timezone = timezone(timedelta(hours=5, minutes=30))

india_time = datetime.now(india_timezone)

print("India time:", india_time)
```

For applications that work across many geographic time zones, the standard `zoneinfo` module is preferable.

```py
from datetime import datetime
from zoneinfo import ZoneInfo

mumbai_time = datetime.now(
    ZoneInfo("Asia/Kolkata")
)

print("Mumbai time:", mumbai_time)
```

You can convert the same moment to another time zone:

```py
from datetime import datetime
from zoneinfo import ZoneInfo

mumbai_time = datetime.now(
    ZoneInfo("Asia/Kolkata")
)

new_york_time = mumbai_time.astimezone(
    ZoneInfo("America/New_York")
)

print("Mumbai:", mumbai_time)
print("New York:", new_york_time)
```

**Important:** A timezone-aware datetime contains timezone information. A naive datetime does not.

---

## Adding and Subtracting Dates

We can use `timedelta` to move dates forward or backward.

```py
from datetime import date, timedelta

date_value = date(2026, 8, 15)

print(date_value + timedelta(days=1))
print(date_value + timedelta(days=7))
print(date_value - timedelta(days=1))
```

Output:

```text
2026-08-16
2026-08-22
2026-08-14
```

We can also add hours to a `datetime`:

```py
from datetime import datetime, timedelta

now = datetime.now()

after_two_hours = now + timedelta(hours=2)

print("Now:", now)
print("After two hours:", after_two_hours)
```

---

## Comparing Dates

Date and datetime objects can be compared using normal comparison operators.

```py
from datetime import date

date1 = date(2026, 8, 15)
date2 = date(2026, 9, 1)

print(date1 < date2)
print(date1 > date2)
print(date1 == date2)
```

Output:

```text
True
False
False
```

This is useful when checking:

- Whether a deadline has passed
- Whether a record belongs to a particular date range
- Whether a file was modified recently
- Whether a scheduled job should run
- Whether data belongs to a specific reporting period

---

## Practical Data Engineering Example

Date and time operations are common in data engineering.

For example, suppose records contain an ingestion timestamp:

```py
from datetime import datetime

records = [
    {"id": 1, "name": "Amit", "ingested_at": "2026-08-15 10:30:00"},
    {"id": 2, "name": "Priya", "ingested_at": "2026-08-15 11:45:00"},
]
```

Convert the string timestamps into datetime objects:

```py
from datetime import datetime

for record in records:
    record["ingested_at"] = datetime.strptime(
        record["ingested_at"],
        "%Y-%m-%d %H:%M:%S"
    )

print(records)
```

You can then compare timestamps:

```py
from datetime import datetime, timedelta

cutoff_time = datetime.now() - timedelta(hours=1)

recent_records = [
    record
    for record in records
    if record["ingested_at"] >= cutoff_time
]

print(recent_records)
```

Date handling is commonly used for:

- Incremental data loading
- Watermark columns
- Partition filtering
- Log processing
- Batch processing windows
- Event timestamps
- Data quality checks
- Reporting periods

---

## Common Date and Time Mistakes

### Mistake 1: Confusing `strftime()` and `strptime()`

Incorrect:

```py
datetime.strptime(datetime.now(), "%Y-%m-%d")
```

`strptime()` expects a string.

Correct:

```py
datetime.strptime("2026-08-15", "%Y-%m-%d")
```

### Mistake 2: Using the Wrong Format

```py
from datetime import datetime

date_string = "15/08/2026"

date_object = datetime.strptime(
    date_string,
    "%m/%d/%Y"
)
```

The format above does not match the intended day/month order.

Correct:

```py
date_object = datetime.strptime(
    date_string,
    "%d/%m/%Y"
)
```

### Mistake 3: Ignoring Time Zones

When applications work across multiple countries, storing and comparing naive local times can produce incorrect results.

For distributed systems, APIs, and data pipelines, timezone-aware timestamps are usually safer.

---

🌕 You are doing well. You have completed Day 16 and now have a solid foundation for working with dates, times, timestamps, durations, and time zones.

## 💻 Exercises: Day 16

### Exercises: Level 1

1. Get the current day, month, year, hour, minute, second, and timestamp from the `datetime` module.
2. Format the current date using this format:

```py
"%m/%d/%Y, %H:%M:%S"
```

3. Today is **15 August 2026**. Convert this string into a `datetime` object:

```py
"15 August, 2026"
```

4. Calculate the time difference between today and New Year's Day:

```text
1 January 2027
```

5. Calculate the time difference between **1 January 1970** and now.
6. Create a date for 30 days from today.
7. Create a date for 30 days before today.

### Exercises: Level 2

8. Convert the following string into a datetime object:

```py
"15/08/2026 18:30:45"
```

9. Convert the datetime object back into this format:

```text
15-Aug-2026 06:30 PM
```

10. Create a timezone-aware datetime for `Asia/Kolkata`.
11. Convert the current India time to New York time using `zoneinfo`.
12. Given two datetime values, calculate the difference in hours and minutes.
13. Given a list of records containing timestamps, filter only records from the last 24 hours.

### Exercises: Level 3

14. Create a function called `days_until()` that accepts a future date and returns the number of days remaining.
15. Create a function called `add_days()` that accepts a date and number of days and returns the new date.
16. Create a function that converts a timestamp into a readable datetime.
17. Create a function that converts a datetime string into a Unix timestamp.
18. Given employee records containing `joining_date`, calculate how many days each employee has been with the company.
19. Given transaction records containing timestamps, group the records by date.
20. Create a small data-ingestion example where records are filtered using an ingestion-time watermark.

### What can you use the `datetime` module for?

Examples:

- Time-series analysis
- Creating timestamps for application events
- Adding posts to a blog
- Data pipeline scheduling
- Incremental data loading
- Watermark-based ingestion
- Log processing
- Partition filtering
- Data quality checks
- Reporting periods
- Calculating processing durations

🎉 CONGRATULATIONS! 🎉

[<< Day 15](../Day_15_Python_type_errors/15_Python_type_errors.md) | [Day 17 >>](../Day_17_Exception_handling/17_Exception_handling.md)
