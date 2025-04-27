# Data Tracker Macros

Macros exist to provide a method of easily adding data entries based on the date or value of other entries.

You can access the Macro page by visiting *Profile -> Macros* where you can create, edit, view and run macros.

Once you have at least one, you will also see a *Run Macros* button in the day view

## Macro Formulas

Formulas use the evaluate() function of mathjs which is extremely powerful. There are some examples below but feel free to research the function and see what else you can do. 

If you reference a category that has no entry for that date, it defaults to 0. 

### Formula Examples

Set as True if Either of These are True

```
[Pickleball] + [Rock Climb] > 0
```
Other Examples
```
[Push Ups] + 3 * (7 - 4)
```
```
sqrt([Pull Ups]) + pow(2, 3)
```

## Macro Schedule (Cron)

Cron is a common and widely documented syntax, feel free to reference other sources for more examples and information.

The cron expression is only evaluated when the macro runs -- not used for scheduling it outright, so it would rarely make sense to change hour, minute, or second from the default '*'.

The schedule feature uses @breejs/later to evaluate the cron syntax when the macro runs. 

### Cron Syntax
```
*    *    *    *    *    *
|    |    |    |    |    |
|    |    |    |    |    +----- Day of week (0 - 7) (Sunday=0 or 7)
|    |    |    |    +---------- Month (1 - 12)
|    |    |    +--------------- Day of month (1 - 31)
|    |    +-------------------- Hour (0 - 23)
|    +------------------------- Minute (0 - 59)
+------------------------------ Second (0 - 59)
```

### Cron Examples
Every Time it Runs
```
* * * * * *
```

Every Saturday
```
* * * * * SAT
```

Every Weekday
```
* * * * * 1,2,3,4,5
```

Every Weekend Day
```
* * * * * SAT,SUN
```

Every First of the Month
```
* * * 1 * *
```

Every Day in January
```
* * * * 1 *
```